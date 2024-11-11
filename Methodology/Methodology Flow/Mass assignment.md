# Mass assignment

Its categorized as a modern vulnerability which occurs when whole object is passed into an updated or create database query. The methodology to find it 

- Look for the data returning URLs, collect all objects and fields
- Identify state changing requests, such as create or update various properties
- Try to add object keys in the state changing requests
- Sometimes, hidden parameter discovery is useful to get an unexpected result

```
POST /v1/merchant/account

{
			"name": "ali",
			"email": "ali@ali.com",
			"**FUZZ**": "test"
}
```

###