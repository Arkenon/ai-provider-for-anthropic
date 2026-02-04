# Anthropic AI Provider

An Anthropic (Claude) provider for the [PHP AI Client](https://github.com/WordPress/php-ai-client) SDK. Works as both a Composer package and a WordPress plugin.

## Requirements

- PHP 7.4 or higher
- [wordpress/php-ai-client](https://github.com/WordPress/php-ai-client) must be installed

## Installation

### As a Composer Package

```bash
composer require wordpress/anthropic-ai-provider
```

### As a WordPress Plugin

1. Download the plugin files
2. Upload to `/wp-content/plugins/anthropic-ai-provider/`
3. Ensure the PHP AI Client plugin is installed and activated
4. Activate the plugin through the WordPress admin

## Usage

### With WordPress

The provider automatically registers itself with the PHP AI Client on the `init` hook. Simply ensure both plugins are active and configure your API key:

```php
// Set your Anthropic API key (or use the ANTHROPIC_API_KEY environment variable)
putenv('ANTHROPIC_API_KEY=your-api-key');

// Use the provider
$result = AiClient::prompt('Hello, world!')
    ->usingProvider('anthropic')
    ->generateTextResult();
```

### As a Standalone Package

```php
use WordPress\AiClient\AiClient;
use WordPress\AnthropicAiProvider\Provider\AnthropicProvider;

// Register the provider
$registry = AiClient::defaultRegistry();
$registry->registerProvider(AnthropicProvider::class);

// Set your API key
putenv('ANTHROPIC_API_KEY=your-api-key');

// Generate text
$result = AiClient::prompt('Explain quantum computing')
    ->usingProvider('anthropic')
    ->generateTextResult();

echo $result->toText();
```

## Supported Models

This provider dynamically discovers available models from the Anthropic API. Current flagship models include:

**Claude 4.5 Series (Latest)**
- `claude-opus-4-5` - Most intelligent model, state-of-the-art coding
- `claude-sonnet-4-5` - Best balance of intelligence, speed, and cost
- `claude-haiku-4-5` - Fast and efficient

**Claude 4 Series**
- `claude-opus-4-1` - Previous flagship model
- `claude-sonnet-4` - Balanced performance
- `claude-opus-4` - High capability

## Configuration

The provider uses the `ANTHROPIC_API_KEY` environment variable for authentication. You can set this in your environment or via PHP:

```php
putenv('ANTHROPIC_API_KEY=your-api-key');
```

## License

GPL-2.0-or-later
