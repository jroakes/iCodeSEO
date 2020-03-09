# Chrome DevTools

Chrome DevTools is a set of web developer tools built directly into the [Google Chrome](https://www.google.com/chrome/) browser. DevTools can help you edit pages on-the-fly and diagnose problems quickly, which ultimately helps you build better websites, faster.

Check out the video for live demonstrations of core DevTools workflows, including debugging CSS, prototyping CSS, debugging JavaScript, and analyzing load performance.

## Open DevTools <a id="open"></a>

There are many ways to open DevTools, because different users want quick access to different parts of the DevTools UI.

* When you want to work with the DOM or CSS, right-click an element on the page and select **Inspect** to jump into the **Elements** panel. Or press Command+Option+C \(Mac\) or Control+Shift+C \(Windows, Linux, Chrome OS\).
* When you want to see logged messages or run JavaScript, press Command+Option+J \(Mac\) or Control+Shift+J \(Windows, Linux, Chrome OS\) to jump straight into the **Console** panel.

See [Open Chrome DevTools]() for more details and workflows.

## Get started <a id="start"></a>

If you're a more experienced web developer, here are the recommended starting points for learning how DevTools can improve your productivity:

* [View and Change the DOM](https://developers.google.com/web/tools/chrome-devtools/dom)
* [View and Change a Page's Styles \(CSS\)]()
* [Debug JavaScript](https://developers.google.com/web/tools/chrome-devtools/javascript)
* [View Messages and Run JavaScript in the Console](https://developers.google.com/web/tools/chrome-devtools/console/get-started)
* [Optimize Website Speed](https://developers.google.com/web/tools/chrome-devtools/speed/get-started)
* [Inspect Network Activity]()

## Discover DevTools <a id="discover"></a>

The DevTools UI can be a little overwhelming... there are so many tabs! But, if you take some time to get familiar with each tab to understand what's possible, you may discover that DevTools can seriously boost your productivity.

### Device Mode <a id="device-mode"></a>

Simulate mobile devices.

* [Device Mode](https://developers.google.com/web/tools/chrome-devtools/device-mode)
* [Test Responsive and Device-specific Viewports](https://developers.google.com/web/tools/chrome-devtools/device-mode/emulate-mobile-viewports)
* [Emulate Sensors: Geolocation & Accelerometer](https://developers.google.com/web/tools/chrome-devtools/device-mode/device-input-and-sensors)

### Elements panel <a id="elements"></a>

View and change the DOM and CSS.

* [Get Started With Viewing And Changing The DOM](https://developers.google.com/web/tools/chrome-devtools/dom)
* [Get Started With Viewing And Changing CSS]()
* [Inspect and Tweak Your Pages](https://developers.google.com/web/tools/chrome-devtools/inspect-styles)
* [Edit Styles]()
* [Edit the DOM](https://developers.google.com/web/tools/chrome-devtools/inspect-styles/edit-dom)
* [Inspect Animations]()
* [Find Unused CSS]()

### Console panel <a id="console"></a>

View messages and run JavaScript from the Console.

* [Get Started With The Console](https://developers.google.com/web/tools/chrome-devtools/console/get-started)
* [Using the Console]()
* [Interact from Command Line](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference)
* [Console API Reference](https://developers.google.com/web/tools/chrome-devtools/console/console-reference)

### Sources panel <a id="sources"></a>

Debug JavaScript, persist changes made in DevTools across page reloads, save and run snippets of JavaScript, and save changes that you make in DevTools to disk.

* [Get Started With Debugging JavaScript](https://developers.google.com/web/tools/chrome-devtools/javascript)
* [Pause Your Code With Breakpoints](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints)
* [Save Changes to Disk with Workspaces](https://developers.google.com/web/tools/setup/setup-workflow)
* [Run Snippets Of Code From Any Page](https://developers.google.com/web/tools/chrome-devtools/snippets)
* [JavaScript Debugging Reference](https://developers.google.com/web/tools/chrome-devtools/javascript/reference)
* [Persist Changes Across Page Reloads with Local Overrides](https://developers.google.com/web/updates/2018/01/devtools#overrides)
* [Find Unused JavaScript]()

### Network panel <a id="network"></a>

View and debug network activity.

* [Get Started](https://developers.google.com/web/tools/chrome-devtools/network-performance)
* [Network Issues Guide](https://developers.google.com/web/tools/chrome-devtools/network-performance/issues)
* [Network Panel Reference](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference)

### Performance panel <a id="performance"></a>

Find ways to improve load and runtime performance.

* [Optimize Website Speed](https://developers.google.com/web/tools/chrome-devtools/speed/get-started)
* [Get Started With Analyzing Runtime Performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance)
* [Performance Analysis Reference](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference)
* [Analyze runtime performance](https://developers.google.com/web/tools/chrome-devtools/rendering-tools)
* [Diagnose Forced Synchronous Layouts](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/forced-synchronous-layouts)

### Memory panel <a id="memory"></a>

 Profile memory usage and track down leaks.

* [Fix Memory Problems](https://developers.google.com/web/tools/chrome-devtools/memory-problems)
* [JavaScript CPU Profiler](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/js-execution)

### Application panel <a id="application"></a>

Inspect all resources that are loaded, including IndexedDB or Web SQL databases, local and session storage, cookies, Application Cache, images, fonts, and stylesheets.

* [Debug Progressive Web Apps](https://developers.google.com/web/tools/chrome-devtools/progressive-web-apps)
* [Inspect and Manage Storage, Databases, and Caches](https://developers.google.com/web/tools/chrome-devtools/manage-data/local-storage)
* [Inspect and Delete Cookies](https://developers.google.com/web/tools/chrome-devtools/manage-data/cookies)
* [Inspect Resources](https://developers.google.com/web/tools/chrome-devtools/manage-data/page-resources)

### Security panel <a id="security"></a>

Debug mixed content issues, certificate problems, and more.

* [Understand Security Issues](https://developers.google.com/web/tools/chrome-devtools/security)

The best place to file feature requests for Chrome DevTools is the mailing list. The team needs to understand use cases, gauge community interest, and discuss feasibility before implementing any new features.



# Additionnal tips

## Comparing raw HTML and rendered HTML

Easily compare the raw HTML of a page and the rendered code with [this plugin](https://chrome.google.com/webstore/detail/view-rendered-source/ejgngohbdedoabanmclafpkoogegdpob).  
It also provides a _diff_ feature to see line by line what has been modified in the DOM by JavaScript.  
