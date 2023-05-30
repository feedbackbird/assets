# FeedbackBird Assets Repository

This repository contains the assets used by FeedbackBird, a SaaS platform for collecting user feedback. These assets include JavaScript files and other resources needed for integrating FeedbackBird into your website or application.

## jsDelivr

jsDelivr is a global content delivery network (CDN) that hosts popular JavaScript libraries and assets. It provides a reliable and efficient way to deliver files to users by distributing the files across multiple servers located around the world. This improves the performance and availability of the assets, ensuring that users can access them quickly and reliably.

## WordPress Integration

To integrate FeedbackBird with a WordPress website, you can use the following example code:

```php
add_action('admin_enqueue_scripts', function () {
    wp_enqueue_script('feedbackbird-app-script', 'https://cdn.jsdelivr.net/gh/feedbackbird/assets@master/wp/app.js?uid=YOUR_UID');
    wp_add_inline_script('feedbackbird-app-script', sprintf('var feedbackBirdObject = %s;', json_encode([
        'userid' => get_current_user(),
        'meta' => [
            'php_version' => PHP_VERSION,
            'active_plugins' => array_map(function ($plugin, $pluginPath) {
                return [
                    'name' => $plugin['Name'],
                    'version' => $plugin['Version'],
                    'status' => is_plugin_active($pluginPath) ? 'active' : 'deactivate',
                ];
            }, get_plugins(), array_keys(get_plugins())),
        ]
    ])));

    add_filter('script_loader_tag', function ($tag, $handle, $src) {
        if ('feedbackbird-app-script' === $handle) {
            return preg_replace('/^<script /i', '<script type="module" id="feedbackbird-app-script" crossorigin="crossorigin"', $tag);
        }
        return $tag;
    }, 10, 3);
});
```

Replace the URL in `wp_enqueue_script` with the appropriate version or specific branch/tag as needed.

## Vanilla HTML Integration

Coming soon...

## Craft CMS Integration

Coming soon...

## Contributing

If you have any suggestions, bug reports, or would like to contribute to the development of the assets, feel free to open an issue or submit a pull request in this repository.

## License

The assets in this repository are licensed under the [MIT License](LICENSE).

---

Feel free to update the "Coming soon" sections with the relevant integration instructions for Vanilla HTML and Craft CMS as you develop them.
