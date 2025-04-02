# Searching and filter 

## Types
There are many techonolgy are popular for using searching and filtering

- Using Spring JPA Specification: 
    - Good for database queries in relational databases
- Using ElasticSearch/Solr
    - full-text search ==> handling large datasets

# Sample code

- JPA Specification
    1. Create DTO custom filtering 
    ```java
    @Getter
    @Setter
    public class ProductSearchCriteria {
        private String name;
        private String brand;
        private BigDecimal minPrice;
        private BigDecimal maxPrice;
        private Long categoryId;
        private Boolean inStock;
    }
    ```
    2. Make repository extends JpaSpecificationExecutor with class of entity
    ```java
    @Repository
    public interface ProductRepository extends JpaRepository<Product, Long>, JpaSpecificationExecutor<Product> {

    }
    ```
    3. Create custom Specification class based on fields of entity
    ```java
    @Configuration
    public class ProductSpecification {

        public Specification<Product> getSearchSpecification(ProductSearchCriteria criteria) {
            return (root, query, cb) -> {
                List<Predicate> predicates = new ArrayList<>();

                if (criteria.getName() != null && !criteria.getName().isEmpty()) {
                    predicates.add(cb.like(cb.lower(root.get("name")),
                            "%" + criteria.getName().toLowerCase() + "%"));
                }

                if (criteria.getBrand() != null && !criteria.getBrand().isEmpty()) {
                    predicates.add(cb.like(cb.lower(root.get("brand")),
                            "%" + criteria.getBrand().toLowerCase() + "%"));
                }

                if (criteria.getMinPrice() != null) {
                    predicates.add(cb.greaterThanOrEqualTo(
                            root.get("price"), criteria.getMinPrice()));
                }

                if (criteria.getMaxPrice() != null) {
                    predicates.add(cb.lessThanOrEqualTo(
                            root.get("price"), criteria.getMaxPrice()));
                }

                if (criteria.getCategoryId() != null) {
                    predicates.add(cb.equal(root.get("category").get("id"),
                            criteria.getCategoryId()));
                }

                if (criteria.getInStock() != null) {
                    if (criteria.getInStock()) {
                        predicates.add(cb.greaterThan(root.get("inventory"), 0));
                    } else {
                        predicates.add(cb.equal(root.get("inventory"), 0));
                    }
                }

                return cb.and(predicates.toArray(new Predicate[0]));
            };
        }

    }
    ```

    4. Finally use it in service!
    ```java
    @Override
    public Page<ProductResponseDTO> searchProducts(ProductSearchCriteria criteria, Pageable pageable) {
        Specification<Product> spec = productSpecification.getSearchSpecification(criteria);
        return productRepository.findAll(spec, pageable).map(autoProductMapper::toResponseDTO);
    }
    ```


