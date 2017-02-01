**Enabling/Disabling guest authentication** (only api key is needed)

**Enable**

In apps tab Assign a Default Role set a role

**Disable**

make sure no Default Role is set 

**Headers**


    headers: new Headers({
      "X-DreamFactory-API-Key": dreamfactoryconfig.APP_API_KEY,
        "X-DreamFactory-Application-Name": dreamfactoryconfig.APP_NAME,
        "X-DreamFactory-Session-Token": token
      })

**Explained:**

Only `"X-DreamFactory-API-Key": dreamfactoryconfig.APP_API_KEY` is needed for guest access

All three are need for authenticated access

    "X-DreamFactory-API-Key": dreamfactoryconfig.APP_API_KEY,
        "X-DreamFactory-Application-Name": dreamfactoryconfig.APP_NAME,
        "X-DreamFactory-Session-Token": token



