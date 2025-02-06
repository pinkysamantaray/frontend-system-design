# What is Frontend System Design?

Imagine you are building a lemonade stand. 
The front of your stand is what people see and interact with—it has a menu, a place to order, and maybe even a cool sign with your name on it. This is like the frontend of a website or app!

Now, let's break it down into simple parts:

**The Stand (UI - User Interface)**
    This is what your customers see. It includes the menu (buttons and text), the counter (forms and input boxes), and the decorations (colors and images). Just like how a bright and fun stand makes people want to buy lemonade, a good UI makes people enjoy using a website or app.

**The Helper (Frontend Logic & Interactivity)**
    Imagine a helper at your stand who takes the order, writes it down, and passes it to the kitchen. This helper makes sure everything runs smoothly. On a website, this is JavaScript! It makes buttons clickable, updates prices, and helps the page respond when you do something.

**The Kitchen (Backend - but still important for frontend!)**
    When a customer orders, the lemonade has to be made in the kitchen. The kitchen (backend) does the real work, but the customer only sees the lemonade arriving. The frontend talks to the backend to get things like data from a database (like checking how many lemons are left).

**Delivery System (APIs & Data Fetching)**
    If your lemonade stand runs out of lemons, you might call a fruit store to bring more. In websites, APIs are like that store—they bring the right information when needed, like showing new posts on social media or checking if a username is available.

**Make It Pretty & Fast (Performance & Design)**
    If your lemonade stand is slow or messy, customers won't like it. The same goes for websites! The frontend has to load quickly, look nice, and work smoothly on phones and computers.

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
    - API Refresher: windows, document, node
        Element.prototype ~= DOM API 
        HTMLDocument.prototype ~= DOM API
    - Querying methods comparison: 
        ![querying methods](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/querying-methods.png)
    - Optimizing query performance 
        Simplify Selectors, use of IDs, pick the right start point of query
3. Web Observer APIs for Complex UI Patterns 
    1. Intersection Observer 
        - Virtualization 
        - Lazy Components 
        - Analytics 
        - Dynamic UI Elements 
        Example: https://codepen.io/RayEuji/embed/wvZJvKN
    2. Mutation Observer 
        - Rich Text Editors 
        - Drawing Tools 
        Example: https://codepen.io/RayEuji/embed/ExJWaEO
    3. Resize Observer 
        - Adaptive Design 
        - Charting tools 
        - Drawing tools
        Example: https://codepen.io/RayEuji/embed/QWPprNE

4. Virtualisation 
    Virtualization is a UI optimization technique that involves maintaining a data in memory while rendering only a limited subset, often referred to as a 'sliding window' 
    Goals of the pattern: 
        1. Minimize number of elements rendered in the DOM Tree 
        2. Minimize number of DOM Mutations 
        3. Minimize CPU & Memory usage that is required to maintain a DOM Tree  

    Pattern: _Top Virtualisation => Bottom Virtualisation_ 
        Initial Loading => Rendering first page => Scrolldown > Selecting Elements to recycle > Recycling Item 1 Item 2 ...Recycling finished => Update the data Top Observer viewport Empty => Update Observers position
        Scrolldown - Load new data => Scrolldown limit reached, Selecting Elements to recycle and so on...
    
5. Application State design 
    - Data classes > UI State 
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

    - Data Properties 
        - Access level 
        - Read/ Write 
        - Frequency Size

    General Principles:
    - Search / Access Optimization: 
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
        - Minimize Search cost, Use _Indexes_ if in-app search is required
        - Minimize RAM usage
    - Memory Offloading: Offload data to hard-drive when it's needed
    - Browser Storage API Overview: Pick a suitable storage
        ![WebStorage types and comparisons.](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/web_storage.png)

6. Network 
    - Browser Networking 
    - Protocols Overview 
    ![protocols overview](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/protocols-overview.png)
    ![protocols types](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/protocols-types.png)
    - Talking to server 
        - Long-polling: Easy & cheap to implement, Battery inefficient (High CPU usage due to open TCP connection and transmitter usage), Network & Data inefficient. Avoid in Mobile web application
        - Server Sent Events: fast, automatic reconnection, Battery efficient, Minimal network overhead (you only receive the actual data without header overhead). Limitation is only string data is supported - you’ll have to parse the payload. can be an alternative to WebSockets when some minor latency is acceptable. Avoid in simple desktop apps, you'll be fine with long-polling
        - Web-sockets: provide almost real-time communication mechanism, Unlimited number of connections. But high infrastructure cost. Web-Sockets are stateful, computing resource ineffeciency. needs to maintain a constant TCP connection, drains energy and utilizes CPU. Works best with machine sensors/controls, Online gaming, Trading, precise location tracking etc.
         
    - REST vs GraphQL:
    GraphQL provides the most value in Complex Apps, can reduce the complexity but needs additional client library to work with server GraphQL API, Additional client caching layer, Additional state manager - GraphQL Client needed to sync state between server and client. Potential impact on your web-bundle size
    ![REST vs GraphQL](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/REST-vs-GraphQL.png)

7. Web Application Performance
    ![Web Vitals](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/Web-Vitals.png)

    Network Performance:
    `<link rel="preload">` - preloads a resource in background with a high priority. `<link rel="prefetch">` - preloads and caches a resource in background with a low priority.
    `defer` (Load when every other asset is ready)
    - Javascript > Bundle concatenation, Bundle Spliting, Advanced prefetching, Code Minification & Compression(gzip, brotli)
    - CSS > Bundle Split, Minification and compression, Fetching critical/non-critical styles, Inline critical resources/styles
    `<link rel="preload" as="style" href="..."/>`
    `<link rel="stylesheet" media="print" href="..." onload="this.media='all'"/>`

    - Images > 
        Compessed SVG(less characters/optimized, less size)
        webp designed to replace png, jpg and gif for usage on the web pages, 
        AVIF: new image encoding format has the same benefits of webp with even better compression and picture quaility
    - Other Assets:
        Fonts: allow browser to display content when custom font is downloading
        ![Font Loading Optimization](https://github.com/pinkysamantaray/frontend-system-design/blob/main/assets/images/Font-Loading-Optimization.png)


Cheers!

----------------------------------------------------------------------------

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.