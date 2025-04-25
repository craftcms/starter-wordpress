# WordPress Starter Project for Craft CMS

This repository contains a complete [Craft CMS](https://craftcms.com) application, configured to closely mirror a default [WordPress](https://wordpress.org) installation. It can be used as an introduction to Craft’s content tools, or as a way to quickly import content from an existing WordPress site.

> [!TIP]  
> See our [Craft CMS for WordPress Developers](https://craftcms.com/knowledge-base/for-wordpress-devs) article for additional information about making the switch to Craft!

## Features

- Sensible defaults that match WordPress content structure;
- Ready-to-use templates for common WordPress content types;
- Live Preview configured out of the box;
- Pre-packaged with our official WordPress [import tool](#importing-content);

## Prerequisites

- [DDEV](https://ddev.com/) or an equivalent local development environment that meets Craft’s [system requirements](https://craftcms.com/docs/5.x/requirements.html);
- A publicly-reachable WordPress site to migrate from, with [administrator-level](https://learn.wordpress.org/lesson/user-management-2/) access;

## Installation

1. Clone this repository and move into the folder:

   ```bash
   git clone https://github.com/craftcms/starter-wordpress.git
   cd starter-wordpress/
   ```

2. Start DDEV:

   ```bash
   ddev start
   ```

3. Install dependencies:

   ```bash
   ddev composer install
   ```

4. Run the Craft setup wizard:

   ```bash
   ddev craft install
   ```

Congratulations—Craft has been installed! You can explore the control panel by opening `https://starter-wordpress.ddev.site/admin` in your browser, or continue reading to import existing content.

> [!NOTE]  
> If you want to use a different subdomain/prefix for this DDEV project, update the `name` key in `.ddev/config.yaml`.

## Preparing Your WordPress Site

Before migration, you'll need to prepare your WordPress site. See the [wp-import repository](https://github.com/craftcms/wp-import) for complete documentation.

1. Install the import helper:
   - Save [`plugins/wp-import-helper.php`](https://github.com/craftcms/wp-import/blob/main/plugins/wp-import-helper.php) to your WordPress site's `wp-content/plugins/` folder
   - Log into WP Admin Dashboard
   - Navigate to **Plugins** and activate "wp-import helper"

2. Create an application password:
   - In WP Admin Dashboard, go to Users
   - Edit an administrator's account
   - Scroll to "Application Passwords"
   - Enter "Craft CMS" as the name
   - Click "Add New Application Password"
   - Save the username and generated password for later use (you'll need it on the import step)

3. Configure custom post types (if applicable):
   - Ensure `'show_in_rest' => true` is set in any calls to `register_post_type()`

4. Configure ACF fields (if applicable):
   - Enable "Show in REST API" for each field group

## Importing Content

The import process is covered in detail in our Craft CMS for WordPress Developers article, but the critical steps are as follows:

1. Run the import script:

   ```bash
   ddev craft wp-import
   ```

2. Enter your WordPress site details when prompted:

   - WordPress site URL
   - Admin username
   - Application password (created earlier)

The importer will create:

- A "Posts" section for your posts
- A "Pages" section for your pages
- An "Uploads" filesystem and volume for your media
- A "Post Content" CKEditor field with nested entry types for non-HTML block data

See the [wp-import repository](https://github.com/craftcms/wp-import) for complete documentation, command options, and compatible fields.

## Next Steps

We encourage you to explore the control panel at your own pace—if you need some guidance, check out this [post-import tour](https://craftcms.com/knowledge-base/for-wordpress-devs#tour).

### Start Templating

This project includes a bare-bones front-end built with Craft’s native template system, [Twig](https://craftcms.com/docs/5.x/development/twig.html). Templates are stored in the `templates/` directory—you are welcome to use them as-is, modify them to suit, or remove them entirely and experiment with the [GraphQL API](https://craftcms.com/docs/5.x/development/graphql.html)!

> [!NOTE]  
> Some template names and locations are significant—they may be factored in to [routing](https://craftcms.com/docs/5.x/system/routing.html), or used by a [section](https://craftcms.com/docs/5.x/reference/element-types/entries.html#sections).

### Push Changes

To push the code to your own repository, you must replace the default _remote_:

```bash
git remote remove origin
git remote add https://github.com/my-organization/my-repo.git
```

If the importer created any new resources (typically resulting in new or updated files in `config/project/`), commit those before pushing!

### Deploy

Read our guide on [hosting and deployment](https://craftcms.com/docs/5.x/deploy.html), or get started with our first-party hosting platform [Craft Cloud](https://craftcms.com/cloud) by spinning up a 7-day free trial:

1. Run the Cloud setup command:

   ```bash
   ddev craft cloud/setup
   ```

1. Commit and [push](#push-changes) those changes to a repository you control;
1. Sign up for [Craft Console](https://console.craftcms.com);
1. Create a new Cloud project;

See our [Getting Started on Craft Cloud](https://craftcms.com/knowledge-base/cloud-getting-started) for details.

## Getting Help

If you have any questions or suggestions, you can always reach us at <support@craftcms.com> or [post a GitHub issue](https://github.com/craftcms/starter-wordpress/issues).

Thanks for trying Craft!

:lemon:
