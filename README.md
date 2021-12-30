# ReactBytes




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
