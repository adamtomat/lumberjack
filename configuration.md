# Configuration

Lumberjack comes with a selection of config files out-of-the-box. These live in the `config/` directory and are simple `.php` files that return an `array`.

### Accessing Configuration Values {#accessing-configuration-values}

Let's take a look at `config/app.php`:

```text
return [    /**     * The current application environment     */    'environment' => getenv('WP_ENV'),​    // ...etc];
```

Here we are proxying an environment variable defined in the `.env` file that Bedrock provides. We'd recommend following this pattern, where you should only see `getenv` called in your config files.

You can easily access the environment variable using the `Rareloop\Lumberjack\Facades\Config` facade.

```text
use Rareloop\Lumberjack\Facades\Config;​$env = Config::get('app.environment');
```

You can provide a default value too, incase the configuration option does not exist.

```text
$env = Config::get('app.environment', 'production');
```

If you need to update a config option, you can use the `set` method, like so:

```text
Config::set('app.debug', false);
```

### Adding your own config files {#adding-your-own-config-files}

Chances are, you're going to need to add your own config files at some point. All you need to do is create a new `.php` file in the `config/` directory, and have it return an array.

This works because Lumberjack will look for all files in the `config/` directory that have a `.php` extention and automatically registers all the data to the application's config.

