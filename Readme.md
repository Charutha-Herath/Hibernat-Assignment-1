Annotations used :

**@Entity** : Used to identify an a class as an entity in a database.

**@Id** : used to identify the primary key of a table or an entity.

**@Generated Value** : Generates a value based on the strategy it is given 

**@GeneratedValue(strategy = GenerationType.IDENTITY)** : This is used to generate a value based on the auto-increment
function in database

**@Column** : Allows to rename a column as given in the column annotation
ex : @Column(name = "author_id")

**@OneToMany(mappedBy = "author" ,orphanRemoval = true,cascade = CascadeType.ALL)** : Notes a one to many relationship
with another table. mapped by function provides a foreign key reference to the other table.
orphanRemoval function provides access to delete any child rows if the parent is deleted. cascade = cascadeType.ALL 
provides cascading functions to delete parent rows along with it's children.

**@OnDelete(action = onDeleteAction.CASCADE)** : Provides basically the on delete cascade function in MySQL but forces 
hibernate to provide the same result as Hibernate JPA does not have delete cascade.

**@ManyToOne** : Notes a Many to one relationship with another table supposedly with another one to many relationship.

**@JoinColumn(name = "auth_id",referencedColumnName = "author_id")** : Joins a column to the given table based on the 
reference it is given by the "referencedColumnName".

HQL Answers 
1.Hibernate: select b1_0.id,b1_0.auth_id,b1_0.price,b1_0.publicationYear,b1_0.title from Book b1_0 where b1_0.publicationYear>?
3   |  Egiptu Shapaya   |   Chandana Mendis    |   800.0    |   2013  |


2. Enter Author id ; 1
   Hibernate: update Book set price=(price+((price/100)*10)) where auth_id=?
   Updated Rows : 1

3. Auther Id : 1
Hibernate: delete from Author where author_id=?
Authors deleted :1

4.Hibernate: select avg(b1_0.price) from Book b1_0
[749.625]

5. Hibernate: select a1_0.name,count(b1_0.id) from Author a1_0 left join Book b1_0 on a1_0.author_id=b1_0.auth_id group by a1_0.author_id
   J.R.R Tolkein:  Count  1
   Chandana Mendis:  Count  2

6. Enter a country : Sri_Lanka
   Hibernate: select b1_0.id,b1_0.auth_id,b1_0.price,b1_0.publicationYear,b1_0.title from Book b1_0 join Author a1_0 on a1_0.author_id=b1_0.auth_id where a1_0.country=?
   | 2| Baskerville Ruduru Balla| 2006| 699.25
   | 3| Egiptu Shapaya| 2013| 800.0

7.   @ManyToOne
     @JoinColumn(name = "auth_id",referencedColumnName = "author_id")
     private Author author;

10. Hibernate: select a1_0.author_id,a1_0.country,a1_0.name from Author a1_0 join Book b1_0 on a1_0.author_id=b1_0.auth_id group by a1_0.author_id having count(b1_0.id)>(select avg(derived1_0.bookCount) from (select count(b2_0.id) from Book b2_0 group by b2_0.auth_id) derived1_0(bookCount))
    Chandana Mendis
#   H i b e r n a t e - A s s i g n m e n t - 1
