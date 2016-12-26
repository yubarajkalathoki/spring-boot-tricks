# spring-boot-tricks
Tricks for spring boot development

You can find here spring-bood development tricks.

***

```java
public List<Response> searchParentDocument(String sort, int size, int page, String search) {
	Sort sortObj = new Sort(new Order(Direction.ASC, sort));
	Pageable pageable = new PageRequest(page, size, sortObj);
	Page<Response> documents = responseRepository.findByNameContaining(search, pageable);
	List<Response> documentList = new ArrayList<>(documents.getContent());
	return documentList;
}
```
