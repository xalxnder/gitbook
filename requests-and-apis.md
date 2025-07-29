---
description: How to use the requests module to access APIs
---

# Requests & APIs

For this example, we'll be using GitHub's API. In a lot of API tutorials, they use the curl command. For me, this was confusing because I'm working mostly with Python.  So for example: `curl https://api.github.com/zen`

```python
>>> import requests 
>>> response = requests.get("https://api.github.com/zen")
>>> print(response)
<Response [200]>
```

