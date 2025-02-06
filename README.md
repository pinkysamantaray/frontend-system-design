### Observer API 
1. Intersection: 
    - Virtualization 
    - Lazy Components 
    - Analytics 
    - Dynamic UI Elements 

    Example: https://codepen.io/RayEuji/embed/wvZJvKN

2. Mutation: 
    - Rich Text Editors 
    - Drawing Tools 

    Example: https://codepen.io/RayEuji/embed/ExJWaEO

3. Resize:
    - Adaptive Design 
    - Charting tools 
    - Drawing tools

    Example: https://codepen.io/RayEuji/embed/QWPprNE

### Virtualization
Virtualization is a UI optimization technique that involves maintaining a data in memory while rendering only a limited subset, often referred to as a 'sliding window' 
Goals of the pattern: 
    1. Minimize number of elements rendered in the DOM Tree 
    2. Minimize number of DOM Mutations 
    3. Minimize CPU & Memory usage that is required to maintain a DOM Tree  

### Data classes and properties
Data classes > UI State 
- App Config 
    1. User theme 
    2. Locale 
    3. font-size 
    4. accessibility settings 
- UI Elements State 
    1. Selected controls 
    2. Selected Text formatting (Google Docs) 
    3. Any other elements configuration 
    4. Entered text etc.
- Server Data 
    1. Messages 
    2. Post 

Data Properties 
- Access level 
- Read/ Write 
- Frequency Size
    
### Application State: 
General Principles:
- Minimize Access cost > 
    Data Normalization: 1F, 2F, 3F etc..(Optimized Access Performance, Optimized Storage Structure, High Developer Readability and Maintenance)

    **1F** > Data is atomic, It has primary key
    ```
    {   
        id: "1",  
        name: "Evgenii",  
        job: {     
            id: "UIE",     
            title: "UI Engineer",     
            department: "Engineering"  
        },  
        location: { 
            code: "UK", 
            name: "United Kingdom" 
        } 
    } 
    =>
    {  
        id: "1",  
        name: "Evgenii", 
        job_id: "UIE",   
        job_title: "UI Engineer",  
        department: "Engineering",  
        country_code: "UK",  
        country_name: "United Kingdom" 
    }
    ```
    **2F** > 1NF + non-primary keys depend on entity primary key
    ```
    const users = { 
        "1": {   
            name: "Evgenii", 
            job_id: 'UIE', 
            country_id: "UK"
        }
    }
    const jobs = { 
        UIE: { 
            title: "UI Engineer", 
            department: 'Engineering' 
        }
    }
    const user_jobs = { 
        "1": "UIE" 
    }; 
    const countries = { 
        UK: "United Kingdom" 
    }
    ```
    **3F** >  2NF + non-primary keys ONLY depend on entity primary key
    ```
    const users = { 
        "1": { name: "Evgenii", job_id: 'UIE', country_id: "UK",  } 
    } 
    const jobs = { 
        UIE: "UI Enginer" 
    }; 
    const department = { 
        UIE: "Engineering"
    };  
    const user_jobs = {
        "1": "UIE" 
    }; 
    const countries = { 
        UK: "United Kingdom" 
    };
    ```

- Minimize Search cost, Use _ _Indexes_ _ if in-app search is required
- Minimize RAM usage
- Offload data to hard-drive when it's needed
- Pick a suitable storage
    /assets/images/web-storage.png

