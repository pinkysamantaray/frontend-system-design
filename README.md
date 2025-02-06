# What is Frontend System Design?

Imagine you are building a lemonade stand. 
The front of your stand is what people see and interact with—it has a menu, a place to order, and maybe even a cool sign with your name on it. This is like the frontend of a website or app!

Now, let’s break it down into simple parts:

**The Stand (UI - User Interface)**
    This is what your customers see. It includes the menu (buttons and text), the counter (forms and input boxes), and the decorations (colors and images). Just like how a bright and fun stand makes people want to buy lemonade, a good UI makes people enjoy using a website or app.

**The Helper (Frontend Logic & Interactivity)**
    Imagine a helper at your stand who takes the order, writes it down, and passes it to the kitchen. This helper makes sure everything runs smoothly. On a website, this is JavaScript! It makes buttons clickable, updates prices, and helps the page respond when you do something.

**The Kitchen (Backend - but still important for frontend!)**
    When a customer orders, the lemonade has to be made in the kitchen. The kitchen (backend) does the real work, but the customer only sees the lemonade arriving. The frontend talks to the backend to get things like data from a database (like checking how many lemons are left).

**Delivery System (APIs & Data Fetching)**
    If your lemonade stand runs out of lemons, you might call a fruit store to bring more. In websites, APIs are like that store—they bring the right information when needed, like showing new posts on social media or checking if a username is available.

**Make It Pretty & Fast (Performance & Design)**
    If your lemonade stand is slow or messy, customers won’t like it. The same goes for websites! The frontend has to load quickly, look nice, and work smoothly on phones and computers.

So, just like making a great lemonade stand, designing a frontend system is about making it easy to use, fast, and fun so people enjoy their experience! 🍋😃

## Table of Contents
1. Core Fundamentals 
    - Box Model:
        Box anatomy(Content box, padding box, border box, margin box), 
        Box size(Intrinsic: content determines space, Restricted: size governed by set of rules), 
        Box type(Block, Inline, Anonymous)
    - Positioning System: position: static | relative | absolute | sticky | fixed
    - Formatting Context: Flex, Grid, Inline, Block...
    - Stacking Context: 
        Single layer is with X and Y Axis. 3D transformation, absolute positioning, or any action that moves an element from the normal flow, we activate an additional axis known as the Stacking Context or Z-axis.
        All CSS Transformations are GPU accelerated, meaning the browser doesn't need to recalculate the DOM Tree when such operations are performed. This minimizes the reflow cycle.
    - Browser Rendering Cycle and Reflow 
    - Composition Layers: 
        DOM Tree > Render Object Tree > Render Layer Tree(when placed in position absolute for example, or transform animations, video or canvas etc) > Graphic Layer
        ![Composition Layers Overview](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/browser-composition-layers.png)
    - GPU Acceleration 
2. DOM API 
    - API Refresher 
    - Querying methods comparison 
    - Optimizing query performance 
3. Web APIs for Complex UI Patterns 
    - Observer API Overview 
    - Intersection Observer 
    - Mutation Observer 
    - Resize Observer 
4. Virtualisation 
    - Pattern overview 
    - Application State design 
    - Search / Access Optimization 
    - Browser Storage API Overview 
    - Memory Offloading
6. Network 
    - Browser Networking 
    - Protocols Overview 
    - Talking to server 
        - Long-polling 
        - Web-sockets 
        - SSE 
    - REST / GraphQL
7. Web Application Perfomrance
    - Javascript 
    - CSS 
    - Images 
    - Other Assets

## Table of Contents
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
        UIE: "UI Engineer" 
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
    ![WebStorage types and comparisons.](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/web_storage.png)


### 
preload
prefetch
defer
example:
 <link rel="preload" as="style" href="..."/>
 <link rel="stylesheet" media="print" href="..." onload="this.media='all'"/>


 font-display:"";