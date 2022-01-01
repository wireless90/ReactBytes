# ReactBytes

My React Learning Snippets

  - [Get Request](#get-request)
  - [Local Storage](#local-storage)
  - [Handling Promise States](#handling-promise-states)


## Get Request
```jsx
import React, { useState, useEffect } from 'react';

export default function GitHubUser({ username }) {
    const [data, setData] = useState();

    /* Fetches the data if username changes */
    useEffect(() =>
    {
        if(userNameEmptyOrNull(username))
            return;
        
        if(dataBelongsToUser(data, username))
            return;
        
        const uri = `https://api.github.com/users/${username}`

        fetch(uri)
            .then(response => response.json())
            .then(setData)
            .catch(console.error);

    }, [username]);

    if(data)
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
    
    return null;
}

/* Private functions */

function dataBelongsToUser(data, username)
{
    return data && data.login === username;
}

function userNameEmptyOrNull(username)
{
    return !username;
}




```

## Local Storage

```jsx
import React, { useState, useEffect } from 'react';

export default function GitHubUser({ username }) {
    const [data, setData] = useState(getJsonFromLocalStorage(username));

    /* Fetches the data if username changes */
    useEffect(() =>
    {
        if(userNameEmptyOrNull(username))
            return;
        
        if(dataBelongsToUser(data, username))
            return;
        
        const uri = `https://api.github.com/users/${username}`

        fetch(uri)
            .then(response => response.json())
            .then(setData)
            .catch(console.error);

    }, [username]);

    /* Saves data if data changes */
    useEffect(() =>
    {
        if(noData(data))
            return;
        
        const { name, avatar_url, location } = data;

        storeDataToLocalStorage(username, {name, username, avatar_url, location });

    }, [data]);

    if(data)
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
    
    return null;
}

/* Private functions */
function getJsonFromLocalStorage(key)
{
    return key && JSON.parse(localStorage.getItem(key));
}

function storeDataToLocalStorage(key, data)
{
    key && localStorage.setItem(key, JSON.stringify(data));
}


function noData(data)
{
    return !data;
}



```

## Handling Promise States

```jsx
import React, { useState, useEffect } from 'react';

export default function GitHubUser({ username }) {
    const [data, setData] = useState(getJsonFromLocalStorage(username));
    const [error, setError] = useState();
    const [loading, setLoading] = useState(false);

    /* Fetches the data if username changes */
    useEffect(() =>
    {
        if(userNameEmptyOrNull(username))
            return;
        
        if(dataBelongsToUser(data, username))
            return;
        
        setLoading(true);

        const uri = `https://api.github.com/users/${username}`

        fetch(uri)
            .then(response => response.json())
            .then(setData)
            .catch(console.error);

    }, [username]);

    /* Saves data if data changes */
    useEffect(() =>
    {
        setLoading(false);
        if(noData(data))
            return;
        
        const { name, avatar_url, location } = data;

        storeDataToLocalStorage(username, {name, username, avatar_url, location });

    }, [data]);

    if(loading)
        return <h1>Loading ...</h1>;
    if(error)
        return <pre>{JSON.stringify(error, null, 2)}</pre>;
    if(!data)
        return null;
    
    return (

       <div className='githubUser'>
           <img src={data.avatar_url} alt={data.login} style={{width: "200px"}} />

           <div>
               <h1>{data.login}</h1>
               {data.name && <p>{data.name}</p>}
               {data.location && <p>{data.location}</p>}
           </div>
       </div>
    );
}

/* Private functions */
function getJsonFromLocalStorage(key)
{
    return key && JSON.parse(localStorage.getItem(key));
}
function userNameEmptyOrNull(username)
{
    return !username;
}
function storeDataToLocalStorage(key, data)
{
    key && localStorage.setItem(key, JSON.stringify(data));
}

function dataBelongsToUser(data, username)
{
    return data.login === username
}

function noData(data)
{
    return !data;
}




```
