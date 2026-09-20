# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: LoginUsingConfig.spec.ts >> Login using config file
- Location: tests\LoginUsingConfig.spec.ts:25:7

# Error details

```
Test timeout of 30000ms exceeded.
```

```
Error: locator.fill: Target page, context or browser has been closed
Call log:
  - waiting for locator('#input-email')

```

# Test source

```ts
  1  | import { Page, Locator } from '@playwright/test';
  2  | 
  3  | export class LoginPage {
  4  | 
  5  |     private readonly page: Page;
  6  | 
  7  |     // Locators
  8  |     private readonly txtEmailAddress: Locator;
  9  |     private readonly txtPassword: Locator;
  10 |     private readonly btnLogin: Locator;
  11 |     private readonly txtErrorMessage: Locator;
  12 | 
  13 | 
  14 |  constructor(page: Page) {
  15 |         this.page = page;
  16 |         
  17 |         // Initialize locators with CSS selectors
  18 |         this.txtEmailAddress = page.locator('#input-email');
  19 |         this.txtPassword = page.locator('#input-password');
  20 |         this.btnLogin = page.locator('input[value="Login"]');
  21 |         this.txtErrorMessage=page.locator('.alert.alert-danger.alert-dismissible');
  22 |     }
  23 | 
  24 |      /**
  25 |      * Sets the email address in the email field
  26 |      * @param email - Email address to enter
  27 |      */
  28 |     async setEmail(email: string){
> 29 |         await this.txtEmailAddress.fill(email);
     |                                    ^ Error: locator.fill: Target page, context or browser has been closed
  30 |     }
  31 | 
  32 |      /**
  33 |      * Sets the password in the password field
  34 |      * @param pwd - Password to enter
  35 |      */
  36 |     async setPassword(pwd: string) {
  37 |         await this.txtPassword.fill(pwd);
  38 |     }
  39 | 
  40 |      /**
  41 |      * Clicks the login button
  42 |      */
  43 |     async clickLogin(){
  44 |         await this.btnLogin.click();
  45 |     }
  46 | 
  47 |      /**
  48 |      * Performs complete login action
  49 |      * @param email - Email address to enter
  50 |      * @param password - Password to enter
  51 |      */
  52 |     async login(email: string, password: string){
  53 |         await this.setEmail(email);
  54 |         await this.setPassword(password);
  55 |         await this.clickLogin();
  56 |     }
  57 | 
  58 |     async getloginErrorMessage():Promise<null | string>{
  59 |        
  60 |         return(this.txtErrorMessage.textContent());
  61 |     }
  62 | 
  63 | 
  64 | 
  65 | 
  66 | 
  67 | 
  68 | 
  69 | 
  70 | }
```