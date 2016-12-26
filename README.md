# spring-boot-tricks
Tricks for spring boot development

You can find here spring-bood development tricks.

***

### 1. Request to jpa repository to search results with sorting and paging.

Here you can see `searchDocument(...)` method has four arguments. Which are `sort` field name, `size` total number of record to be fetched, `page` whether page number is 1 or 2 or 3 and so on and `search` is the value of document name. Here we are naming `documentRepository` method as `findByNameContaining(String search, Pageable pageable)`. It means `documentRepository` finds document containing `search` value and returns the result with sorting by sort (field) value and returns the number of `size`.

```java
public List<Document> searchDocument(String sort, int size, int page, String search) {
	Sort sortObj = new Sort(new Order(Direction.ASC, sort));
	Pageable pageable = new PageRequest(page, size, sortObj);
	Page<Document> documents = documentRepository.findByNameContaining(search, pageable);
	List<Document> documentList = new ArrayList<>(documents.getContent());
	return documentList;
}
```
