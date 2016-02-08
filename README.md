# Cache WP_Query
Cache WP_Query will cache posts from WP_Query through an automatic wrapper. It avoids extra DB requests and caches to object cache. Integrates with ElasticPress to cache those requests too!

## Supports

* ElasticPress
* Pods (utilizing Pods caches)
* Pods Alternative Cache (through Pods support, you can cache your query results to the filesystem)

## Usage

In your `WP_Query` arguments, set `'cache_wp_query' => true`.

```php
$args = array(
	'post_type'      => 'posts',
	/* complicated arguments with meta lookups, date queries, etc */
	'cache_wp_query' => true, // Cache this query
);

$my_query = new WP_Query( $args );
```

In your plugin or theme, add the post types you want to support for caching (this is primarily for cache clearing purposes when a new post is published). By default, no post types are cached until you add support for one.

```php
/**
 * Add support to my post types for Cache WP Query
 */
function my_cache_wp_query_post_types() {

	add_post_type_support( 'post', 'cache_wp_query' );
	add_post_type_support( 'my_cpt', 'cache_wp_query' );

}
add_filter( 'init', 'cache_wp_query_post_types' );
```

Searches are cached by default (assuming post types are all in the list above), but this can be disabled.

```php
// Disable default search caching
add_filter( 'cache_wp_query_search', '__return_false' );
```
