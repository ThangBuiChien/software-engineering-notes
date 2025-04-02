# Table of Contents

[Bi-directional mapping](#inheritance-and-polymorphism)

[Fetching stategy](#fetching-stategy)

[Best practises](#constructors-and-garbage-collection)

# Bi-directional mapping

## Examples

```java
  public class Product{
    @ManyToOne(fetch = FetchType.LAZY, optional = false )
    @JoinColumn(name = "category_id", nullable = false)
    private Category category;
  }

  public class Category{
    @OneToMany(mappedBy = "category", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Product> products = new ArrayList<>();
  }
```

## Best practises

    1. Add helper methods to maintain the bidirectional relationship (In the non-owning side)

```java
  public class Category{
    public void addProduct(Product product){
        this.products.add(product);
        product.setCategory(this);
        // With CascadeType.ALL, this will also save the product, just use categoryRepository.save(category)
    }

    public void removeProduct(Product product){
        this.products.remove(product);
        product.setCategory(null);
    }
  }
```

2. Consider using fetch type LAZY for the non-owning side to avoid loading all the related entities when not needed.

```java
  public class Category{
    @OneToMany(mappedBy = "category", cascade = CascadeType.ALL, orphanRemoval = true, fetch = FetchType.LAZY)
    private List<Product> products = new ArrayList<>();
  }
```

## fetching-stategy

### Default strategy

| LAZY         | EAGER       |
| ------------ | ----------- |
| one-to-many  | one-to-one  |
| many-to-many | many-to-one |

- => ... to many : LAZY
- => ... to one : EAGER

- But use carefully with LAZY which could potentially cause **LazyInitializationException**

### Why LAZY is better

- EAGER => Really bad performance, load all the related entities when the parent entity is loaded
- LAZY could potentially cause **LazyInitializationException** but it's better to handle it than having bad performance

### LazyInitializationException

- This exception is thrown when an uninitialized collection or proxy is accessed outside of the scope of the Session, which is the case when the session is closed or the transaction is committed.

```java
@Service
public class CourseService {
    @Autowired
    private CourseRepository courseRepository;

    // This will cause LazyInitializationException
    public void wrongWay() {
        Course course = courseRepository.findById(1L).orElseThrow();
        // Transaction ends here

        // This line throws LazyInitializationException
        // because we're accessing lazy collection outside transaction
        List<Student> students = course.getStudents();
        students.forEach(student -> System.out.println(student.getName()));
    }
}
```

- There many ways to fix it

  - 2 bad ways are
    - Open Session in View => keeps the Hibernate session open for the entire duration of a web request, including during view rendering
    - hibernate.enable_lazy_load_no_trans => Hibernate is allowed to fetch lazy-loaded entities even after the session has been closed (outside a transaction). It does this by keeping the session partially alive.
  - 2 reconmend ways, but need to create custom queries

    - JOIN FETCH or EntityGraph
    - DTO projection

  - The easiest way is to use @Transactional => This will keep the session open until the end of the method
