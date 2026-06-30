Part A: Test Structure

describe():
Purpose: Groups related individual test cases into a single organized box or section(INDEX)


Syntax: describe('Description of the suite', () => {

});

Example: describe('Amazon Shopping Cart functionality', () => {

});

Real-world use case: Putting all the tests for the “Sign Up” page in one place so your code stays neat and easy to find.

it():
Purpose: Defines an individual, specific test case block inside your organized section (INDEX)

Syntax: it('Description of what this specific test should do', () => {

});

Example: it('Should display an error when the password is too short', () => {

});

Real-world use case: Testing just the “Submit” button on a feedback form to make sure it sends the message when clicked.

before():
Purpose: Runs your setup code exactly one time  before any of the tests in that section start (INDEX)
Syntax: before(() => {

});
Example: before(() => {
  cy.log('Setting up global test database seed data')
})
Real-World Use Case: Seeding a testing database with standard product items or clearing system server logs once before running a 50-test checkout suite.

beforeEach():
Purpose: Runs automatically before every single individual test starts.
Syntax: beforeEach(() => {

});

Example: beforeEach(() => {
  cy.visit('https://netflix.com');
});

Real-world use case:
Opening the login screen before every test case so each test always starts fresh from the exact same page.

after():
Purpose: Runs cleanup code exactly one time after all the testsb in that section are completely finished. 
Syntax: after(() => {

});

Example: after(() => {
  cy.log('Closing all open connections')
})

Real-world use case: Deleting temporary data records or generating a global test coverage execution report at the absolute end of a test run.

afterEach():
Purpose: Runs automatically after every single individual test finishes.
Syntax: afterEach(() => {

});
Example: afterEach(() => {
  cy.clearCookies();
});
Real-world use case: Clearing out browser cookies or logging out after each test so the next test doesn’t accidentally stay logged into the wrong profile.

Part B: Assertions
Assertions are checkpoints in your test to verify if what is happening on the website matches what you expect 

Difference Between the two:
should() (Implicit): It is built directly into Cypress commands and is chained directly to a page element. It automatically retries over and over until it passes or times out.

expect() (Explicit): It stands on its own inside a custom function block. It does not retry; it checks the data exactly once immediately when it is called.
                
            When to use each:
Use should() when you are checking things directly on the screen (like testing if a button is visible, if an input box contains text, or if a checkbox is checked)
Use expect() when you are checking background data,variables, numbers, custom logic, or responses from an API instead of a visual element.

Three Examples for each: 
should()

Example 1: Check if an element is visible
cy.get('.search-button').should('be.visible')
Example 2: Check the text value of an input box
cy.get('#username').should('have.value', 'student123')
Example 3: Check if a checkbox is selected
cy.get('[type="checkbox"]').should('be.checked')

         expect()
             Example 1: Check if a text variable matches a specific name
             cy.get('.product-name').then(($el) => {
                 const laptopName = $el.text()
                 expect(laptopName).to.equal('MacBook Pro')
             })
             Example 2: Check if a count or number matches
             const itemCount = 5
             expect(itemCount).to.equal(5)
             Example 3: Check if a variable is true
             const isPageLoaded = true
             expect(isPageLoaded).to.be.true


         Part C: Basic Cypress Commands


Action
Command
Example
Visit a page
cy.visit()
cy.visit(‘https://google.com’)
Type into a textbox
cy.type()
cy.get(‘#input’).type(‘hello’)
Click a button
cy.click()
cy.get('.btn').click()
Clear a field
cy.clear()
cy.get('#username').clear()
Check a checkbox
cy.check()
cy.get('#agree-terms').check()
Uncheck a checkbox
cy.uncheck()
cy.get('#agree-terms').uncheck()
Select from a dropdown
cy.select()
cy.get('#country').select('USA')
Scroll to an element
cy.scrollIntoView()
cy.get('#footer').scrollIntoView()
Upload a file
cy.selectFile()
cy.get('#file-upload').selectFile('file.pdf')
Hover over an element
cy.trigger('mouseover')
cy.get('.menu-item').trigger('mouseover')
Right click
cy.rightclick()
cy.get('.context-menu').rightclick()
Double click
cy.dblclick()
cy.get('.edit-icon').dblclick()
Press keyboard keys
cy.type('{keyname}')
cy.get('body').type('{enter}')




             Part D: Locators
cy.get()
Finds one or more elements anywhere on the page using a standard code label (CSS selector).
Syntax: cy.get('selector')
Example: cy.get('.submit-button')
cy.contains()
Finds an element by searching for the actual text written inside it.
Syntax: cy.contains('text')
Example: cy.contains('Log In')
.find()
Searches inside an element you have already located to find a specific child element.
Syntax: cy.get('parent').find('child')
Example: cy.get('.nav-bar').find('img')
.children()
Gets all the immediate elements sitting directly inside a parent box.
Syntax: cy.get('parent').children()
Example: cy.get('.dropdown-menu').children()
.parent()
Moves one step up to find the immediate container enclosing the element.
Syntax: cy.get('child').parent()
Example: cy.get('#username-input').parent()
.closest()
Looks upward through parent containers to find the nearest element matching a specific rule.
Syntax: cy.get('element').closest('selector')
Example: cy.get('input').closest('form')
.eq()
Picks a specific item out of a list of elements based on its index number (starting at 0).
Syntax: cy.get('list').eq(index)
Example: cy.get('.product-item')
.first()
Picks the absolute first item from a list of matching elements.
Syntax: cy.get('list').first()
Example: cy.get('li').first()
.last()
Picks the absolute last item from a list of matching elements.
Syntax: cy.get('list').last()
Example: cy.get('li').last()
.within()
Limits all subsequent commands to only run inside one specific container box.
Syntax: cy.get('box').within(() => { /* commands */ })
Example: 
cy.get('#login-form').within(() => { 
cy.get('input[type="text"]').type('John')
})
1. Why are IDs preferred?
IDs are preferred because they are unique to a single element on a web page. This prevents your script from accidentally selecting or clicking the wrong item.
2. What are CSS selectors?
CSS selectors are the labels used in web development to target elements on a page so they can be styled or automated. They include tag names (button), IDs (#submit), and class names (.btn).
3. What are data attributes (data-cy, data-testid)?
These are custom labels added to HTML code specifically for testing purposes. They isolate your automation script from changes to design classes or structures, keeping your tests from breaking when the website gets a visual update.
4. Why are long CSS selectors discouraged?
Long selectors (like div > ul > li > span > a) are highly fragile. If a developer inserts a small change, like moving a list item or adding an extra container box, the path breaks instantly and causes the automated test to fail.

Part E: Assertions Practice
be.visible
Checks if an element can actually be seen on the screen.
Example:
cy.get('.search-bar').should('be.visible')
exist
Checks if an element exists in the background code (HTML), even if it is hidden from view.
Example:
cy.get('#hidden-popup').should('exist')
contain
Checks if an element includes specific text somewhere inside it, even if there is other text too.
Example:
cy.get('.alert-box').should('contain', 'Success')
have.text
Checks if an element matches a text string exactly, letter for letter.
Example:
cy.get('.header-title').should('have.text', 'Welcome Back')
have.value
Checks the current typed text inside an input field or textbox.
Example:
cy.get('#email-input').should('have.value', 'student@test.com')
have.length
Checks the total number of items in a list or collection.
Example:
cy.get('.product-item').should('have.length', 4)
be.enabled
Checks if a button or input field is clickable and active.
Example:
cy.get('.submit-btn').should('be.enabled')
be.disabled
Checks if a button or input is locked or grayed out so you cannot interact with it.
Example:
cy.get('.submit-btn').should('be.disabled')
be.checked
Checks if a checkbox or radio button has been selected.
Example:
cy.get('#agree-terms').should('be.checked')
have.attr
Checks if an element has a specific structural property, like checking where a link points.
Example:
cy.get('a').should('have.attr', 'href', '/home')
           
           Part F: Working with Elements
Buttons
Finds a button and clicks it to trigger an action.
Example:
cy.get('.login-button').click()
Text fields
Finds a standard text box, clears out any old text, and types new text into it.
Example:
cy.get('#username-field').clear().type('student_user')
Password fields
Locates a secure password input field and enters a sensitive text value.
Example:
cy.get('input[type="password"]').type('MySecurePassword123!')
Checkboxes
Selects an unselected checkbox option and verifies it is successfully checked.
Example:
cy.get('#terms-checkbox').check().should('be.checked')
Radio buttons
Selects a single target option out of a radio button group selection.
Example:
cy.get('[type="radio"]').check('male')
Dropdowns
Selects a specific visible text option or values layout from a choice dropdown menu list.
Example:
cy.get('#country-dropdown').select('United States')

Text areas
Finds a large multiline comments text box box to type a descriptive paragraph message.
Example:
cy.get('textarea#feedback-box').type('This website layout structure is incredibly fast and highly responsive.')

Links
Finds a clickable link path and validates where it redirects users.
Example:
cy.contains('Forgot Password?').click()
cy.url().should('include', '/reset-password')
Images
Locates an image placeholder item component box to make sure the picture asset loaded correctly.
Example:
cy.get('img.profile-picture').should('be.visible')
     Part G: Waiting
Automatic waiting
Cypress automatically waits for elements to exist, become visible, and stop animating before it tries to click or type on them. You do not need to manually add delays for basic page actions.
Retry-ability
If an assertion fails (like checking if a button is visible), Cypress will not crash immediately. It automatically retries the command over and over for up to 4 seconds until the element appears or the test times out.
cy.wait()
A manual command used to pause test execution. It can be used to stop for a hardcoded number of milliseconds, or dynamically wait for an asynchronous background process to finish.
Waiting for API requests
Instead of guessing how long a backend server will take, Cypress can track network requests using cy.intercept(). It pauses the test and resumes the absolute millisecond the server sends back a data response.
Waiting for page loading
When you use commands like cy.visit() or click a link that changes the URL, Cypress automatically pauses execution and waits for the new web page structure to fully load before moving to the next line.
Why is cy.wait(5000) considered bad practice?
It forces the test browser to freeze for  5 seconds, even if the website finishes loading in under half a second. This slows down your automation runs and creates "flaky" tests if the server occasionally takes longer than 5 seconds.
What is a better alternative?
The best alternative is to add a custom timeout directly to your element check.
Instead of freezing the browser for a flat 5 seconds, this tells Cypress to wait up to a certain amount of time, but move on the exact millisecond the element appears.
Example: cy.get('.success-message', { timeout: 6000 }).should('be.visible')
        Part H: Forms
Attached a screenshot of the successful test.
        Part I: Tables
Attached a screenshot of the successful test.



     Part J: Browser Interactions
1. Browser Back
Simulates pressing the "Back" arrow button at the top of your web browser to go to the previous page.
Syntax: cy.go('back')
Example: cy.go('back')
2. Browser Forward
Simulates pressing the "Forward" arrow button at the top of your web browser to return to a page you just went back from.
Syntax: cy.go('forward')
Example:  cy.go('forward')
3. Reload
Refreshes the current web page, just like clicking the circular refresh arrow button or pressing F5 on your keyboard.
Syntax: cy.reload()
Example: cy.reload()
4. Open a New Tab (How Cypress Handles This)
Cypress cannot open or interact with multiple browser tabs at the same time. To bypass this rule, Cypress strips away the code that forces a link to open in a new tab (target="_blank"), forcing the link to load inside the exact same window.
Example:
cy.get('.external-link').invoke('removeAttr', 'target').click()
5. Browser Alerts
Cypress automatically clicks "OK" on standard pop-up alert warning windows. You can catch the text inside the pop-up to verify what it says.
Example:
cy.on('window:alert', (alertText) => {
  expect(alertText).to.equal('Success! Message Sent.')
})
6. Confirmation Dialogs
Cypress automatically accepts confirmation pop-ups (clicks "OK"). You can write an event listener to check the text, or explicitly force it to click "Cancel" instead by returning false.
Example (Clicking Cancel):
cy.on('window:confirm', (confirmText) => {
  expect(confirmText).to.equal('Are you sure you want to delete this?')
  return false // Forces Cypress to click "Cancel" instead of "OK"
})
7. Prompt Dialogs
A prompt dialog box asks the user to type in a text input value. Because Cypress runs automatically, you must intercept the window prompt beforehand and inject a pre-filled fake text answer string.
Example:
cy.window().then((windowItem) => {
  cy.stub(windowItem, 'prompt').returns('My Test Name')
})
     Part K: Keyboard Actions

1. Enter
Simulates pressing the "Enter" key, which is commonly used to submit a form or a search bar without clicking a button.
Example:
cy.get('#search-field').type('clothes{enter}')
2. Tab
Cypress does not natively support the {tab} key inside its standard .type() command to jump between input boxes. To simulate a tab action, you must use a plugin (like cypress-plugin-tab) or manually switch focus to the next element.
Example (Using Plugin):
cy.get('#first-input').tab()
Example (Standard Workaround):
cy.get('#second-input').focus() 
3. Escape
Presses the "Esc" key to dismiss open dropdown menus, close modal pop-up windows, or cancel active overlays.
Example:
cy.get('body').type('{esc}')
4. Arrow Up
Presses the upward directional navigation arrow key, which is useful for scrolling text areas or moving selection lists.
Example:
cy.get('.volume-slider').type('{uparrow}')
5. Arrow Down
Presses the downward directional navigation arrow key to browse custom item selection menu drop-downs.
Example:
cy.get('.dropdown-list').type('{downarrow}')
6. Arrow Left
Presses the left directional key to slide components backward or adjust input ranges leftward.
Example:
cy.get('input[type="range"]').type('{leftarrow}')
7. Arrow Right
Presses the right directional key to slide interactive components forward or adjust ranges rightward.
Example:
cy.get('input[type="range"]').type('{rightarrow}')
8. Delete
Simulates hitting the "Delete" key to remove characters located directly to the right of the typing cursor position.
Example:
cy.get('#username').type('{del}')
9. Backspace
Simulates hitting the "Backspace" key to erase characters located directly to the left of the typing cursor position.
Example:
cy.get('#wrong-input').type('{backspace}')

         Part L: Scrolling
1. Scroll to the Bottom of a Page
Example:   cy.scrollTo('bottom')
2. Scroll to the Top
Example: cy.scrollTo('top')
3. Scroll to a specific element
Example: cy.get('#footer-contact-form').scrollIntoView()
4. Verify the element becomes visible
Example: cy.get('#footer-contact-form').scrollIntoView().should('be.visible')

         Part M: File Upload
1. Why Cypress Cannot Upload Files by Default
Historically, older versions of Cypress lacked native browser commands to interact directly with deep operating system file dialog windows due to strict browser security sandboxes. To bypass this, automated test scripts relied on community-built workarounds to drop file attachments into target page elements.
2. The Plugin or Built-In Approach Commonly Used
The Old Way (Plugin): Developers manually installed a popular external package called cypress-file-upload and used a custom command shortcut (.attachFile()).
The Modern Way (Built-in): Cypress introduced a powerful native command called .selectFile(). You do not need to install any external plugins anymore—this command handles standard files, drag-and-drop areas, and raw data buffers out of the box.
3. Upload a Sample Image or PDF
The built-in .selectFile() command handles both images and PDFs exactly the same way. The only difference is the file name you type at the end of the folder path.
Example 1: Uploading an Image
cy.get('input[type="file"]').selectFile('cypress/fixtures/profile-picture.png')
Example 2: Uploading a PDF
cy.get('input[type="file"]').selectFile('cypress/fixtures/assignment-report.pdf')#

Bonus Challenge
1. cy.intercept()
Monitors, manages, or changes network requests and API responses made by the browser during a test.
What it does: It acts like a traffic cop for network data. It can track backend API calls so your test can wait for them to finish, or it can swap out real data for fake test data.
Example:
cy.intercept('GET', '/api/users').as('getUsers')
cy.visit('/dashboard')
cy.wait('@getUsers') // Dynamically waits for the network to finish loading
2. cy.fixture()
Loads raw mock data saved inside your project files to use in your test cases.
What it does: It reads files (like .json or .png) from your cypress/fixtures/ folder. This keeps large data sets out of your clean test code.
Example:
cy.fixture('user-data.json').then((userData) => {
  cy.get('#email').type(userData.email)
  cy.get('#password').type(userData.password)
})
3. cy.request()
Makes direct HTTP network calls (like GET, POST, or DELETE) without using a visual browser page interface.
What it does: It talks directly to a backend server. This is used to test APIs quickly or to set up data (like logging a user in or deleting an item) before a visual UI test runs.
Example:
cy.request('POST', '/api/items', { name: 'New Test Product' }).then((response) => {
  expect(response.status).to.equal(201) // Verifies server accepted the data
})
4. Custom Cypress Commands
Allows you to create your own reusable shortcut commands to simplify repeating steps.
What it does: Instead of typing the same 5 lines of code to log in or fill out a form in every single test file, you define it once in your commands.js file and call it with a single line.
Example:
Cypress.Commands.add('loginShortcut', (email, pass) => {
  cy.get('#email').type(email)
  cy.get('#password').type(pass)
  cy.get('#submit').click()
})
cy.loginShortcut('student@test.com', 'Pass123!')
5. Page Object Model (POM)
A design pattern where you separate page layout elements and actions from your actual test step scenarios.
What it does: You create a separate JavaScript file for a webpage (like LoginPage.js) containing all its element selectors. If a developer changes a button name, you only update it once in that class file instead of updating 20 different test files.
Example:
class LoginPage {
  visit() { cy.visit('/login') }
  fillUsername(name) { cy.get('#user').type(name) }
}
export default LoginPage
import LoginPage from './pages/LoginPage'
const login = new LoginPage()
it('Should login using POM', () => {
  login.visit()
  login.fillUsername('JohnDoe')
})






















































  




















