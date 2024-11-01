# Authentication

**Description**:

**Input**:

**Expected Output**: 
 1. Successful login message or an error if authentication fails.

**Code Snippet**:
```python
import os
from planet import Auth
# Authenticate with Planet API key
api_key = os.getenv("PL_API_KEY")
auth = Auth.from_key(api_key)
print("Authenticated successfully!")
```
