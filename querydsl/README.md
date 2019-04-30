# QueryDSL examples

참조 : https://bitbucket.org/atlassian/querydsl-examples


# 간단한 insert 구문
```java
    SQLInsertClause insertClause = new SQLInsertClause(connection, PostgreSQLTemplates.DEFAULT, POST);
    insertClause.set(POST.CONTENT, "content")
                .set(POST.TITLE, "title");
```

```sql
    insert into POST (CONTENT, TITLE)
    values (?, ?)
```

# 간단한 insert 구문(삽입된 Item의 Key 반환)
```java
    SQLInsertClause insertClause = new SQLInsertClause(connection, PostgreSQLTemplates.DEFAULT, POST);
    insertClause.set(POST.CONTENT, "content")
                .set(POST.TITLE, "title");
                .executeWithKey(Integer.class);
```

```sql
    insert into POST (CONTENT, TITLE)
    values (?, ?)
```
# 간단한 update 구문
```java
    SQLUpdateClause updateClause = new SQLUpdateClause(connection, PostgreSQLTemplates.DEFAULT, POST);
    updateClause.set(POST.CONTENT, "updated content")
                .set(POST.TITLE, "updated title")
                .where(POST.ID.eq(1l));
```

```sql
    update POST
    set CONTENT = ?, TITLE = ?
    where POST.ID = ?
```
# 간단한 update 구문 (값을 증가 시키는)
```java
    SQLUpdateClause updateClause = new SQLUpdateClause(connection, PostgreSQLTemplates.DEFAULT, POST);
    updateClause
               .set(POST.ID, POST.ID.add(5))
               .where(POST.ID.eq(1l));
```

```sql
    update POST
    set ID = ID + ?
    where POST.ID = ?
```

# 테이블 Join

```java
    query()
        .select(PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME)
        .from(PRODUCT)
        .join(PRODUCT_ITEM)
        .on(PRODUCT_ITEM.PRODUCT_ID.eq(PRODUCT.ID))
        .join(PRODUCT_ITEM_SKU)
        .on(PRODUCT_ITEM_SKU.ID.eq(PRODUCT_ITEM.SKU_ID))
        .orderBy(PRODUCT_ITEM.PRICE.asc());
```

```sql
    select PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME
    from PRODUCT PRODUCT
    join PRODUCT_ITEM PRODUCT_ITEM
    on PRODUCT_ITEM.PRODUCT_ID = PRODUCT.ID
    join PRODUCT_ITEM_SKU PRODUCT_ITEM_SKU
    on PRODUCT_ITEM_SKU.ID = PRODUCT_ITEM.SKU_ID
    order by PRODUCT_ITEM.PRICE asc
```

# 테이블 Left Join

```java
    query()
        .select(PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME)
        .from(PRODUCT)
        .leftJoin(PRODUCT_ITEM)
        .on(PRODUCT_ITEM.PRODUCT_ID.eq(PRODUCT.ID))
        .orderBy(PRODUCT_ITEM.PRICE.asc())
```

```sql
    select PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME
    from PRODUCT PRODUCT
    left join PRODUCT_ITEM PRODUCT_ITEM
    on PRODUCT_ITEM.PRODUCT_ID = PRODUCT.ID
    order by PRODUCT_ITEM.PRICE asc
```

# SQlExpression.select 를 이용한 서브쿼리


```java
    query()
        .select(PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME)
        .from(PRODUCT)
        .join(PRODUCT_ITEM)
        .on(PRODUCT_ITEM.PRODUCT_ID.eq(PRODUCT.ID))
        .join(PRODUCT_ITEM_SKU)
        .on(PRODUCT_ITEM_SKU.ID.eq(PRODUCT_ITEM.SKU_ID))
        .where(
                PRODUCT.NAME.like("drone%")
                        .and(PRODUCT.ID.in(
                                SQLExpressions.select(PRODUCT.ID)
                                        .from(PRODUCT)
                                        .join(PRODUCT_AVAILIBILITY)
                                        .on(PRODUCT_AVAILIBILITY.PRODUCT_ID.eq(PRODUCT.ID))
                                        .where(PRODUCT_AVAILIBILITY.AVAILABLE.eq(true))
                        )))
        .orderBy(PRODUCT_ITEM.PRICE.asc());
```

```sql
    select PRODUCT_ITEM_SKU.SKU_BARCODE, PRODUCT_ITEM.PRICE, PRODUCT.NAME
    from PRODUCT PRODUCT
    join PRODUCT_ITEM PRODUCT_ITEM
    on PRODUCT_ITEM.PRODUCT_ID = PRODUCT.ID
    join PRODUCT_ITEM_SKU PRODUCT_ITEM_SKU
    on PRODUCT_ITEM_SKU.ID = PRODUCT_ITEM.SKU_ID
    where PRODUCT.NAME like ? and PRODUCT.ID in (select PRODUCT.ID
    from PRODUCT PRODUCT
    join PRODUCT_AVAILABILITY PRODUCT_AVAILABILITY
    on PRODUCT_AVAILABILITY.PRODUCT_ID = PRODUCT.ID
    where PRODUCT_AVAILABILITY.AVAILABLE = ?)
    order by PRODUCT_ITEM.PRICE asc
```

# 테이블 alias

```java

    // note that the Q entities are instantiated with aliases in this case
    QEmployee WORKER = new QEmployee("worker");
    QEmployee MANAGER = new QEmployee("manager");

    query()
        .select(WORKER.NAME.as("worker_name"), MANAGER.NAME.as("manager_name"))
        .from(WORKER)
        .join(MANAGER)
        .on(MANAGER.ID.eq(WORKER.MANAGER_ID));
```

```sql
    select worker.NAME as worker_name, manager.NAME as manager_name
    from EMPLOYEE worker
    join EMPLOYEE manager
    on manager.ID = worker.MANAGER_ID
```

# Select for update

Select for update locks the table so you can make a subsequent modification such as an update.

See [Postgres documentation](https://www.postgresql.org/docs/9.0/static/sql-select.html#SQL-FOR-UPDATE-SHARE) for more details

```java
    query()
        .select(PRODUCT.all())
        .forUpdate()
        .from(PRODUCT)
        .orderBy(PRODUCT.NAME.asc())
```

```sql
    select PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE
    from PRODUCT PRODUCT
    order by PRODUCT.NAME asc
    for update
```

# Expressions 를 사용한 현재 시간, 날짜

```java
    query()
            .select(PRODUCT.LAUNCH_DATE, Expressions.currentTime(), Expressions.currentTimestamp())
            .from(PRODUCT)
            .where(PRODUCT.LAUNCH_DATE.before(Expressions.currentDate()))

```

```sql
    select PRODUCT.LAUNCH_DATE, current_time, current_timestamp
    from PRODUCT PRODUCT
    where PRODUCT.LAUNCH_DATE < current_date

```

# Maths expression - max

There are plenty of other Maths expressions such as min(),max(),avg(),round() and so on...

```java
    query()
            .select(PRODUCT_ITEM.PRICE.max())
            .from(PRODUCT_ITEM)

```

```sql
    select max(PRODUCT_ITEM.PRICE)
    from PRODUCT_ITEM PRODUCT_ITEM
```

# 생성자 메소드를 사용하는 Projections


QueryDSL에는 원시 튜플 (JDBC의 ResultSet과 유사)을 특정 Java 클래스에 맵핑하는 기능이 있습니다.


예를 들어 다음과 같은 모델 클래스가 있다고 가정합니다.


```java

    public class ProductDTO {
        private final Long id;
        private final String name;
        private final Date launchDate;
    
        public ProductDTO(Long id, String name, Date launchDate) {
            this.id = id;
            this.name = name;
            this.launchDate = launchDate;
        }
    
        public Long getId() {
            return id;
        }
    
        public Date getLaunchDate() {
            return launchDate;
        }
    
        public String getName() {
            return name;
        }
    }
```

Projections.contstructor를 통해 QueryDSL 에서 반환되는 컬럼을 지정하여 맵핑할수 있습니다.
이 경우 3 개의 매개 변수를 사용하는 ProductDTO의 생성자를 호출합니다.


```java
    query()
            .select(Projections.constructor(
                    ProductDTO.class, PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE)
            )
            .from(PRODUCT)
```

```sql
    select PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE
    from PRODUCT PRODUCT
```

# Bean projection

Should you be using mutable JavaBeans, then you can have QueryDSL project results onto that bean.  

```java

    public class ProductBean {
        private Long id;
        private String name;
        private Date launchDate;
    
        public ProductBean(Long id, String name, Date launchDate) {
            this.id = id;
            this.name = name;
            this.launchDate = launchDate;
        }
    
        public Long getId() {
            return id;
        }
    
        public void setId(Long id) {
            this.id = id;
        }
    
        public Date getLaunchDate() {
            return launchDate;
        }
    
        public void setLaunchDate(Date launchDate) {
            this.launchDate = launchDate;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    }

```

You can then declare your QEntity as being a relational path that produces that bean type.  This is a clue
to system as to what Java types this entity can be bound to.

Note also that this examples is using Pocketknife QueryDSL EnhancedRelationalPathBase.  The
RelationPathBase from native QueryDSL does the same thing.

```java
     public class QProduct extends EnhancedRelationalPathBase<ProductBean> {
     
         public NumberPath<Long> ID = createLongCol("ID").asPrimaryKey().build();
         public StringPath NAME = createStringCol("NAME").build();
         public DatePath<Date> LAUNCH_DATE = createDateCol("LAUNCH_DATE", Date.class).build();
     
         public QProduct() {
             super(ProductBean.class, "PRODUCT");
         }
     }
```

When this runs it will instantiate a new instance of the "type" backing the PRODUCT entity
which as seen above is class ProductBean.
 
The reason this approach is handy is that it means you get results in the Java shape you want.  

```java
    List<ProductDTO> result = query()
            .select(Projections.constructor(
                    ProductDTO.class, PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE)
            )
            .from(PRODUCT)
            .fetch();
```

```sql
    select PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE
    from PRODUCT PRODUCT
```

There is another variant that sets bean fields directly (via reflection) rather than requiring the class
to contain setters.

```java
    query()
            .select(Projections.fields(PRODUCT,
                    PRODUCT.ID, PRODUCT.NAME, PRODUCT.LAUNCH_DATE)
            )
            .from(PRODUCT)
```


# Group by transformation


java object들의 'in memory group by' 가 가능합니다.
여기서 기억해야 할점은 group by는 database 가 아닌 in memory 에서 일어난다는 것 입니다.
그러나 이것은 하나의 인스턴스로 계층적 구조로 읽을때 유용합니다.


```java
            Map<Long, PostDTO> post = query()
                    .from(POST)
                    .join(COMMENT).on(POST.ID.eq(COMMENT.POST_ID))
                    .transform(GroupBy.groupBy(POST.ID).as(
                            Projections.bean(PostDTO.class, POST.ID, POST.TITLE, POST.CONTENT,
                                    GroupBy.set(COMMENT).as("comments"))
                            )
                    );
```

GroupBy.list() 를 사용하여 Post Id 별 Comment 들을 그룹화 할 수 있습니다.

```java
            Map<Long, List<CommentDTO>> result = query()
                    .from(POST)
                    .join(COMMENT).on(POST.ID.eq(COMMENT.POST_ID))
                    .transform(GroupBy.groupBy(POST.ID).as(
                            GroupBy.list(COMMENT))
                    );
```


```sql
    select POST.ID, POST.TITLE, POST.CONTENT
    from POST POST
    join COMMENT COMMENT
    on POST.ID = COMMENT.POST_ID

```



