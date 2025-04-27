# Table of Contents

[1. Example](#example)

[Interface in spring JPA](#jpa-interface)

[Add condition befroe saving to db in entity](#add-condition-before-saving-to-db-in-entity)

# example

# JPA interface

- Use Polymorphic Associations

# Add condition before saving to db in entity

```java
    @PrePersist
    @PreUpdate
    private void validateParent() {
        if ((question == null && answer == null) || (question != null && answer != null)) {
            throw new IllegalStateException("Comment must be attached to either a question or an answer, but not both.");
        }
    }

```

```java
 @AssertTrue(message = "Comment must belong to either a question or an answer, but not both.")
    public boolean isValidParent() {
        return (question != null) ^ (answer != null); // XOR
    }
```
