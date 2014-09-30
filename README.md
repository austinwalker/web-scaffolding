SCSS Project Scaffolding
===============

#### Summary
Hopefully this repo can help you set up your visual styles and structure at the beginning of a project, saving you from bloat, headaches and a thousand cuts later.  I've tried to set out a ~~bare~~ bones scaffolding that gives you enough to get started but doesn't leave around a lot of extra rules without reason.  Please read this document and familiarize yourself with an approach that I've found on past project tends to work quite well.

#### Assumed Situation
I'm assuming you're starting a green field web project, you've been handed the designs and you'll be making the first commits of static markup and styles.

#### Assumed Goals
1. Create an accurate and consistent reproduction of the designer's vision.
2. Write our styles in such a way that it's easy for the rest of the team to achieve Goal #1 without making things overly complex.

#### The Gist
To promote reusability and visual consistency across the site, we want to be able to place markup and classes anywhere on the site and have it look the same regardless of it's location, within reason.  A primary green button should look the same regardless if it's on the homepage, cart page, in an accordion or in the footer.

This is the concept of the approach, to have incredibly reusable styles that can be set up initally and easily reused by multiple team members throughout the project.

#### Folder Structure
- `/ops/` contains mixins or variables for utilization throughout the project.  Code in this folder should not generate actual CSS by itself.`
- `/scaffolding/` holds all our foundational frameworks and global adjustments (think reset, grid, font sources etc).  You probably won't write very much here except for changing the font sources.
- `/vendor/` is where we'll keep our vendor provided CSS.
- `/patterns/` are the smallest bits of repeatable visual items in the site (think icons, buttons, type etc).  Hopefully you can nail this section at the beginning of the project and simply build off of it in `/components/` later.
- `/components/` are large chunks of the site that tend to get repeated (think header, footer, grid item etc)
- `/pages/` contains page specific styles.  Try not to write much here.
- `main.scss` assembles the all the partials.  This should only have `@import` statements.

#### Approach Details & Other Handy Tips
Not hard and fast rules.  Just things that have been helpful in the past.
- Avoid nesting
  - This will create specificy that reduces code reuse and often leads to bloat.
- Use lower case, namespaced and dash deliniated classes
  - Generic - Specific - More Specific
  - Good: `.header-nav-link` `.article-header-byline` `.metric-label`
  - Bad: `.myClass` `.my_class`
- Don't name classes based on thier content
  - Because what happens when you want to put the .404-page-title on the product details page?
  - Good: `.panel-cta` `.graph-title-bar`
  - Bad: `.newsletterSignupButtonRed` `.most-404-hits-monthly-title-bar`
- Don't use IDs unless needed for JS browser support
- Don't overqualify selectors (similar to don't nest)
  - Good: `.header-nav-link`
  - Bad: `a#js-nav.header-nav-link`
- Prefix classes that are targeted with jQuery with 'js-'
  - Good: `.js-video-link` `.js-sort`
  - Bad: `.video-link` `.sort` 
    - These bad examples might be good for CSS, but if JS is hooked here, a team member might accidentally remove it without checking
- Prefix classes that indicate state with 'is-' or 'has-' and style them
  - Example: `.is-active` `.has-error`
- If CSS selectors are written alphabetically, it makes it much easier for everyone to scan
    ```
    Good:

    .header {
    }
    
    .header-menu-icon {
    }

    .header-nav-link {
    }

    Bad:

    .header-nav-link {
    }

    .header {
    }

    .header-menu-icon {
    }
  ```
- Write your CSS rules are written alphabetically, it makes it much easier for everyone to scan
    
    ```
    .article-promo {
      @extend %extensible-placeholder; // Extends first
      @include font-size($fs-lg); // Mixins second
      @include user-select(none);
      background-image: url('img/promo-logo.png'); // Alphabetized rules third
      background-image: url('img/promo-logo.svg');
      background-size: cover;
      border-radius: 5px;
      color: $text-color;
      float: left;
      line-height: 1.2em;
      margin-bottom: 10px;
      padding: 20px;
      z-index: 10;
    }
    ```












