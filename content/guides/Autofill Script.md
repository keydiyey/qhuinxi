
I am sick and tired of typing the same things for career factors. 

1. Make sure [TamperMonkey](https://www.tampermonkey.net/) [[Browsers#Extensions|extension]] is installed.

## Writing the script

1. Create the header for your script. You can customize this however you like.
```js
// ==UserScript==
// @name         autofill the damn job
// @namespace    http://tampermonkey.net/
// @version      2026-02-22
// @description  try to take over the world!
// @author       You
// @match        https://*/*
// @icon         data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==
// @grant        none
// ==/UserScript==
```

2. Go to any career10.successfactors web application and study the website's HTML. Press `ctrl + shift + I` to inspect the website. Take note of the ID, class, or name values of the things you want to fill.

| Target           | Component       | Type | Value             |
| ---------------- | --------------- | ---- | ----------------- |
| Job Specific     | Dropdown Button | ID   | 469:topBar        |
| Notice Period    | Input           | Name | cust_noticePeriod |
| Rate of Pay      | Input           | Name | jobRateOfPay      |
| Salary Expection | Input           | Name | cust_salaryExpect |


3.  This is our main function. It calls other functions that waits for the site to load, searches for the dropdown button, opens it, and fills up the required input boxes. 

``` js
const checkPageReady = setInterval(() => {
        // 1. Check if the document is fully loaded
        if (document.readyState === "complete") {
            // 2. Search for the dropdown button. 
            const targetButton = document.getElementById("469:topBar");
            
            // 3. Runs the functions in sequence
            if (targetButton) {
                clearInterval(checkPageReady); // Stop checking once found
                openthebutton(targetButton);
                fillthedamnpage();
            }}
            
    }, 1000); // Every 1 second
```


3.  Since elements are hidden within dropdowns, we cannot crawl to the input boxes without opening it. This function opens the button if it is closed. 
```js
 async function openthebutton(button) {
        console.log("Page ready. Expanding section...");

        // Expand only if currently closed
        if (button.getAttribute("aria-expanded") === "false") {
            button.click();
            // Wait for the accordion animation and field rendering
            await new Promise(r => setTimeout(r, 800)); }
    }
```

4. This function fills the damn page. Just replace the values to you desired thing. 
	
```js
function fillthedamnpage(){
	document.querySelector('input[name="cust_noticePeriod"]').value = "0";
	document.querySelector('input[name="jobRateOfPay"]').value = "0";
	document.querySelector('input[name="cust_salaryExpect"]').value = "0";

    // Select
    // Do not Change!
	document.querySelector('select[name="cust_currency"]').value = "PHP";
	document.querySelector('input[aria-label="Negotiable (Y/N)"]').type = "Yes";
	document.querySelector('input[aria-label="How did you hear about this job?"]').type = "On-line Job Sites (Jobstreet, Monster, Kalibrr, etc.)";

	// Reference 1
	document.querySelector('input[name="cust_refName1"]').value = "Name";
	document.querySelector('input[name="cust_refOrg1"]').value = "Organization";
	document.querySelector('input[name="cust_refDesig1"]').value = "Role";
	document.querySelector('input[name="cust_refRelationship1"]').value = "Relation";
	document.querySelector('input[name="cust_refContact1"]').value = "Number";
	document.querySelector('input[name="cust_refEmail1"]').value = "Email";

    // Reference 2
	document.querySelector('input[name="cust_refName2"]').value = "Name";
    document.querySelector('input[name="cust_refOrg2"]').value = "Organization";
    document.querySelector('input[name="cust_refDesig2"]').value = "Role";
    document.querySelector('input[name="cust_refRelationship2"]').value = "Relation";
    document.querySelector('input[name="cust_refContact2"]').value = "Number";
    document.querySelector('input[name="cust_refEmail2"]').value = "Email";

    // Reference 3
    // Copy and paste here. You know the pattern. Just replace the number with 3.
    }
```