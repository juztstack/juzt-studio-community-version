# Juzt Studio (Community Version)

Customizer editor for general settings and templates JSON for WordPress.

## 🚀 Installation

### Option 1: Using Composer (Recommended)

```bash
# Navigate to your plugin directory
cd wp-content/plugins/juzt-studio-community

# Install dependencies
composer install
```

### Option 2: Without Composer

The plugin includes a fallback autoloader, so it will work even without Composer. However, using Composer is recommended for better performance.

## 📁 Project Structure

```
juzt-studio-community/
├── composer.json              # Composer configuration
├── juzt-studio-community.php  # Main plugin file
├── .gitignore
├── README.md
└── src/                       # Source files (PSR-4 autoloaded)
    ├── Core.php              # Main core class
    ├── Builder.php           # Admin builder functionality
    ├── Compatibility.php     # Legacy function compatibility
    ├── Sections.php          # Section management
    ├── Snippets.php          # Snippet management
    ├── Templates.php         # JSON template management
    └── TimberExtension.php   # Twig/Timber extensions
```

## 🎯 Usage

### Basic Setup

1. Activate the plugin in WordPress admin
2. The plugin will automatically initialize

### Theme Integration

Add theme support in your theme's `functions.php`:

```php
add_theme_support('sections-builder', [
    'sections_directory' => 'sections',
    'templates_directory' => 'templates',
    'snippets_directory' => 'snippets',
]);
```

### Using Templates

Create a JSON template file in your theme's `templates` directory:

```json
{
    "name": "Home Page",
    "description": "Custom home page template",
    "sections": {
        "hero": {
            "section_id": "hero",
            "settings": {
                "title": "Welcome"
            }
        }
    },
    "order": ["hero"]
}
```

### Rendering Templates

In your page template:

```php
<?php
// The plugin automatically handles template rendering
// Just select the JSON template in the page editor
render_json_template();
?>
```

### Creating Sections

Create a section file in `sections/hero.php`:

```php
<div class="hero-section">
    <h1><?php echo esc_html($settings['title']); ?></h1>
</div>
```

### Using Snippets

Create reusable snippets in `snippets/button.php`:

```php
<button class="btn"><?php echo esc_html($text ?? 'Click me'); ?></button>
```

Use in your templates:

```php
<?php render_snippet('button', ['text' => 'Learn More']); ?>
```

### Global Functions

The plugin provides backward-compatible global functions:

- `render_snippet($name, $data, $return)` - Render a snippet
- `get_snippet($name, $data)` - Get snippet output as string
- `sections_theme_render_section($section)` - Render a section
- `render_json_template()` - Render the current JSON template
- `juzt_studio()` - Get the core instance
- `sections_builder()` - Alias for juzt_studio()

## 🔧 Timber/Twig Integration

If you're using Timber, the plugin automatically registers Twig filters:

```twig
{# In your Twig templates #}
<img src="{{ section.settings.logo|attachment_url }}" 
     alt="{{ section.settings.logo|attachment_alt }}">

{# Or use the attachment function #}
{% set logo = attachment(section.settings.logo) %}
<img src="{{ logo.url }}" alt="{{ logo.alt }}">
```

Available filters:
- `attachment_url` - Get attachment URL
- `attachment_alt` - Get alt text
- `attachment_title` - Get title
- `attachment_caption` - Get caption
- `attachment_srcset` - Get srcset
- `attachment_img` - Generate full img tag

## 📝 Development

### Running Composer

```bash
# Install dependencies
composer install

# Update dependencies
composer update

# Dump autoload (after adding new classes)
composer dump-autoload
```

### PSR-4 Autoloading

All classes follow PSR-4 standard:
- Namespace: `Juztstack\JuztStudio\Community`
- Base directory: `src/`
- Class names match file names

### Adding New Classes

1. Create your class file in `src/` directory
2. Use the namespace `Juztstack\JuztStudio\Community`
3. Run `composer dump-autoload` (if using Composer)

Example:

```php
<?php
namespace Juztstack\JuztStudio\Community;

class MyNewFeature {
    public function __construct() {
        // Your code
    }
}
```

## 🤝 Contributing

This is the community version of Juzt Studio. Contributions are welcome!

## 📄 License

MIT License

## 🔗 Links

- [Juzt Stack](https://juztstack.com)
- [Documentation](https://juztstack.com/docs) (coming soon)

## ⚡ Requirements

- WordPress 5.8+
- PHP 7.4+
- Composer (optional but recommended)