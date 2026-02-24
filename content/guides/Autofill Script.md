>[!Warning] Disclaimer
> I have very minimal **javascript** knowledge so if this code is too cluttered and unoptimized you know why.  

I am sick and tired of typing the same things for career factors. 

-  Make sure [TamperMonkey](https://www.tampermonkey.net/) [[Browsers#Extensions|extension]] is installed.
-  Our roadmap for this script is
	- [[#Waiting for the Page to Load]]
	- [[#Clicking the Dropdown]] 
	- [[#Filling the damn page]]
	- 

# Preliminary

Go to any career10.successfactors web application and study the website's HTML. Press `ctrl + shift + I` to inspect the website. Take note of the ID, class, or name values of the things you want to fill.

| Target           | Component       | Type | Value             |
| ---------------- | --------------- | ---- | ----------------- |
| Job Specific     | Dropdown Button | ID   | 469:topBar        |
| Notice Period    | Input           | Name | cust_noticePeriod |
| Rate of Pay      | Input           | Name | jobRateOfPay      |
| Salary Expection | Input           | Name | cust_salaryExpect |
| ...              | ...             | ...  | ...               |

 Create the header for your script. You can customize this however you like.
 
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

This is our main function. It will contain other functions that waits for the site to load, searches for the dropdown button, opens it, and fills up the required input boxes. 

``` js
const checkPageReady = setInterval(() =>{
	// Put code inside
}, 1000);
```

# Waiting for the Page to Load

 Create an `IF statement` checking if the page is ready.
```js
if (document.readyState === "complete"){ }
```

## Clicking the Dropdown
 
 Since elements are hidden within dropdowns, we cannot crawl to the input boxes without opening it. This function opens the button if it is closed. 
 
Inside the curly braces of the previous `IF statement`, add the following code. This creates a variable for the dropdown button.

```js
const targetButton = document.getElementById("469:topBar");
```

Create another function that presses the dropdown. This function will pass `targetbutton` variable as an argument.

```js
 async function openthebutton(button) {
        console.log("Page ready. Expanding section...");
        // Expand only if closed
        if (button.getAttribute("aria-expanded") === "false") {
            button.click(); //clicks it hihi
            // Wait
            await new Promise(r => setTimeout(r, 800)); }
    }
```

# Filling the damn page

This function fills the damn page. Just replace the values to you desired thing. 
	
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

# Running the functions

Of course we need to run the functions we made. Create another `IF statement` that checks if `targetButton` exists. Once it has been verified, this will run all the functions inside. Put this inside our main function.

```js
if (targetButton) {
		clearInterval(checkPageReady); // Stop checking once found
		openthebutton(targetButton);
		fillthedamnpage();
	}
```

# The Whole Code <3

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

const checkPageReady = setInterval(() =>{
	if (document.readyState === "complete"){ 
		const targetButton = document.getElementById("469:topBar");
		if (targetButton) {
			clearInterval(checkPageReady); // Stop checking once found
			openthebutton(targetButton);
			fillthedamnpage();
		}
	}
}, 1000);

async function openthebutton(button) {
	console.log("Page ready. Expanding section...");
	// Expand only if closed
	if (button.getAttribute("aria-expanded") === "false") {
		button.click(); //clicks it hihi
		// Wait
		await new Promise(r => setTimeout(r, 800)); }
    }

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