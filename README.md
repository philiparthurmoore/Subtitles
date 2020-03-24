# Subtitles WordPress Plugin

[![Gitter](https://badges.gitter.im/wecobble/Subtitles.svg)](https://gitter.im/wecobble/Subtitles?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge) ![Travis CI Build Status](https://travis-ci.org/wecobble/Subtitles.svg?branch=master) [![Maintainability](https://api.codeclimate.com/v1/badges/0a1f6c571a369ebce00b/maintainability)](https://codeclimate.com/github/wecobble/Subtitles/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/0a1f6c571a369ebce00b/test_coverage)](https://codeclimate.com/github/wecobble/Subtitles/test_coverage)

![Subtitles in action](https://i.cloudup.com/YoFzxUCM2S.png)

Add subtitles into your WordPress posts, pages, custom post types, and themes. No coding required. Simply activate _Subtitles_ and you're ready to go.

Right now WordPress currently presents no easy way for web publishers to add subtitles into their posts, pages, and other custom post types. This leaves users and developers in a bit of a quandary, trying to figure out how best to present subtitles in a beautiful and sensible way. Post [excerpts](http://codex.wordpress.org/Function_Reference/the_excerpt) are a very poor choice for subtitles and the only available option outside of [custom fields](http://codex.wordpress.org/Custom_Fields), but custom fields aren't entirely self-explanatory or user-friendly. This simple, straightforward plugin aims to solve this issue.

Simply download _Subtitles_, activate it, and begin adding subtitles into your posts and pages today. For more advanced usage of the plugin, please see the [Frequently Asked Questions](https://github.com/wecobble/Subtitles/blob/master/README.md#frequently-asked-questions).

If you like _Subtitles_, [thank us with coffee](https://www.paypal.me/wecobble) :coffee:. If you find it buggy, [tell us on GitHub](https://github.com/wecobble/Subtitles/issues) :beetle:. And if you have a cool example of how you're using _Subtitles_ on your website, let us know on [Twitter](https://twitter.com/wecobblellc) :bird:.

## Installation

By default the _Subtitles_ plugin just works. All you should need to do in order to begin using it is activate the plugin and begin adding subtitles into your posts, pages, and _Subtitles_-enabled custom post types.

There are no custom template tags to add into your theme and, outside of advanced use, there is nothing you need to do to your theme in order to begin using this plugin.

What follows are instructions on how to install the plugin and get it working.

### Using The WordPress Dashboard (Recommended) ###

1. Navigate to *Plugins → Add New* from within the WordPress Dashboard.
2. Search for `subtitles`.
3. Click **Install Now** on *Subtitles* by We Cobble.
4. Activate the plugin.

### Uploading in WordPress Dashboard ###

1. Navigate to *Plugins → Add New* from within the WordPress Dashboard.
2. Click on the **Upload** link underneath the *Install Plugins* page title.
3. Click the **Browse...** button and choose `subtitles.zip` in its download location on your computer.
4. Click the **Install Now** button.
5. Activate the plugin.

### Using FTP (Not Recommended) ###

1. Download `subtitles.zip`.
2. Extract the `subtitles` directory to your computer.
3. Upload the `subtitles` directory to your `/wp-content/plugins/` directory.
4. Navigate to *Plugins → Installed Plugins* and activate the plugin.

---

## Frequently Asked Questions ##

There are two types of questions that are anticipated: user questions and developer questions. I'll address the user questions first, and then dive into more detailed information about customizing _Subtitles_.

### How to Use _Subtitles_ ###

_Subtitles_ lets you easily add subtitles into your WordPress posts, pages, custom post types, and themes.

![New post waiting on a title and subtitle](https://i.cloudup.com/HhC9q0j5bH.png)

After plugin activation, you should see an input field labeled **Enter subtitle here** immediately under your **Enter title here** input field. After adding a subtitle into your post, simply hit publish and then view your post. There's nothing else to do.

---

### Uninstalling _Subtitles_ ###

When you uninstall _Subtitles_, nothing will happen to your subtitles post meta. They'll still be retained in your database, so if you ever decide to use _Subtitles_ again, you'll be able to activate the plugin and have your subtitles show up. In a future release, there may be the option to clean subtitles out of your database, but it didn't make the cut for the initial release, and auto-deleting the data on uninstallation would have been a bad move, as subtitles are non-trivial post meta.

---

### _Subtitles_ Doesn't Work! ###

There are two primary issues that may cause users to think that _Subtitles_ doesn't work: 1) no subtitles show on the site or 2) weird HTML begins to appear around titles on a site. We will address both of those here.

#### Subtitles Don't Show Up On My Site!

Subtitles relies on two things to work properly: 1) `the_title` being present in your theme and 2) the [WordPress Loop](http://codex.wordpress.org/The_Loop). This plugin works by automatically filtering all appropriate post titles so that you are not put in the position of needing to open your theme files manually and using the [custom template tags](https://github.com/wecobble/Subtitles#using-template-tags) that are available in this plugin.

Some themes use titles outside of the standard WordPress Loop, which means that _Subtitles_ won't touch those. If you would like to use subtitles in a non-standard area of your site, outside of the Loop, then you can either change the views that are [supported by the plugin](https://github.com/wecobble/Subtitles#modifying-supported-subtitles-views) or manually use the template tags that are available to you in this plugin.

The reason this approach has been taken is because if titles outside of the Loop were touched so liberally, you would end up seeing subtitles in places on your site that you wouldn't want them, like in sidebars, navigation menus, and admin screens.

#### There's Weird HTML Showing Up On My Site!

I can almost guarantee that the reason this is happening is because your theme developer is using either `the_title` or `get_the_title` in places where they should not be used. This is a theme bug, not a plugin bug. When titles are used as attributes, the appropriate template tag to use is `the_title_attribute`, never `the_title`.

Please see [these long threads](https://github.com/wecobble/Subtitles/issues?q=the_title_attribute) as examples of what happens when themes conflict with _Subtitles_.

---

### SEO ###

Will _Subtitles_ ruin your SEO? That's a fair question. The answer is no. We've made a note of exactly why `<spans>` are the default wrappers for subtitles in the [inline developer docs](https://github.com/wecobble/Subtitles/blob/master/subtitles.php) for the plugin, which I'll reiterate here:

```php
 * 4. Visually, we have made a major assumption that subtitles belong immediately after titles. The very
 *    definition of a subtitle is that it is a subordinate title of a published work that often gives
 *    explanatory details about the immediately preceeding title. It's for this reason that we've chosen
 *    to filter the output of the_title() with the expectation that post titles will be wrapped in
 *    primary heading (h1) tags. So post titles will be H1, while their subtitles will be spans.
 *    Multiple H1 tags in the HTML5 age are okay.
 * 5. The reason that <spans> are being used is because HTML does not have a dedicated mechanism for
 *    marking up subheadings, alternative titles, or taglines. There are suggested alternatives from
 *    the World Wide Web Consortium (W3C); among them are spans, which work well for what we're trying
 *    to do with titles in WordPress. See the linked documentation for more information.
 *    @link http://www.w3.org/html/wg/drafts/html/master/common-idioms.html#sub-head
```

If you're worried about SEO and the markup of _Subtitles_, then [roll your own markup](https://github.com/wecobble/Subtitles#modifying-subtitles-markup).

---

### Front-End Performance ###

As of version 2.0.0, _Subtitles_ outputs its CSS via `wp_head`. This is to load sensible CSS that will ensure your subtitle is always scaled properly alongside your website title and never shown in comment areas.

```css
/**
 * Plugin Name: Subtitles
 * Plugin URI: http://wordpress.org/plugins/subtitles/
 * Description: Easily add subtitles into your WordPress posts, pages, custom post types, and themes.
 * Author: We Cobble
 * Author URI: https://wecobble.com/
 * Version: 2.1.1
 * License: GNU General Public License v2 or later
 * License URI: http://www.gnu.org/licenses/gpl-2.0.html
 */

/**
 * Be explicit about this styling only applying to spans,
 * since that's the default markup that's returned by
 * Subtitles. If a developer overrides the default subtitles
 * markup with another element or class, we don't want to stomp
 * on that.
 *
 * @since 1.0.0
 */
span.entry-subtitle {
	display: block; /* Put subtitles on their own line by default. */
	font-size: 0.53333333333333em; /* Sensible scaling. It's assumed that post titles will be wrapped in heading tags. */
}
/**
 * If subtitles are shown in comment areas, we'll hide them by default.
 *
 * @since 1.0.5
 */
#comments .comments-title span.entry-subtitle {
	display: none;
}
```

If you'd like to remove this additional CSS, then simply add a similar function to the following in your plugin or theme's primary setup file:

```php
if ( class_exists( 'Subtitles' ) && method_exists( 'Subtitles', 'subtitle_styling' ) ) {
	remove_action( 'wp_head', array( Subtitles::getInstance(), 'subtitle_styling' ) );
}
```

After doing this, no styling should be loaded on the front end of your site and you'll need to style subtitles using your own CSS.

---

### Adding _Subtitles_ Support into Custom Post Types ###

If you'd like to add _Subtitles_ support into a custom post type, use `add_post_type_support` in a function hooked to `init`, for example:

```php
function theme_slug_add_subtitles_support() {
	add_post_type_support( 'custom-post-type-slug', 'subtitles' );
}
add_action( 'init', 'theme_slug_add_subtitles_support' );
```

This should also work on core-supported post types, like `attachment`.

---

### Removing Default Support from Posts and Pages ###

If you'd like to remove _Subtitles_ support from posts or pages, use `remove_post_type_support` in a function hooked to `init`, for example:

```php
function remove_subtitles_support() {
	remove_post_type_support( 'post', 'subtitles' );
	remove_post_type_support( 'page', 'subtitles' );
}
add_action( 'init', 'remove_subtitles_support' );
```

This will work on any post type that may have had _Subtitles_ support added into it elsewhere.

---

### Modifying _Subtitles_ Markup ###

HTML does not have a dedicated mechanism for marking up subheadings, alternative titles, or taglines. There are [suggested alternatives](http://www.w3.org/html/wg/drafts/html/master/common-idioms.html#sub-head) from the World Wide Web Consortium (W3C); among them are spans, which work well for what we're trying to do with titles in WordPress.

If for some reason you'd like to change the markup, hook a custom output function to `subtitle_markup`, for example:

```php
function subtitle_markup_mods( $markup ) {
	$markup[ 'before' ] = '<span class="custom-subtitle-class">';
	$markup[ 'after' ] = '</span>';

	return $markup;
}
add_filter( 'subtitle_markup', 'subtitle_markup_mods' );
```

I do not suggest using headings tags for subtitles.

---

### Displaying _Subtitles_ in RSS Feeds ###

By default subtitles do not show in RSS feeds. If you'd like to show them then the following snippet should help:

```php
/**
 * Show subtitles in RSS feeds.
 */
function display_subtitles_in_rss_feeds() {
	return false;
} // end function display_subtitles_in_rss_feeds
add_filter( 'subtitles_is_feed', 'display_subtitles_in_rss_feeds' );
```

---

### Modifying Supported _Subtitles_ Views ###

By default, subtitles appear on most views throughout a site. This includes single post views, single page views, archive views, and search results pages.

If you'd like to change this behavior, you can do so by taking advantage of `subtitle_view_supported`. For example, if you'd like to hide subtitles on all archive pages, the following code would work:

```php
/**
 * Disable Subtitles in archive views.
 *
 * @see function is_archive
 * @see function in_the_loop
 */
function subtitles_mod_supported_views() {
	// Ditch subtitles in archives.
	if ( is_archive() ) {
		return false;
	}

	// Default in The Loop behavior from Subtitles.
	if ( in_the_loop() ) {
		return true;
	}
} // end function subtitles_mod_supported_views
add_filter( 'subtitle_view_supported', 'subtitles_mod_supported_views' );
```

---

### Allow Developers to Override the Early Bailout if No Subtitle Exists. ###

By default, the plugin will bail out early if no subtitle is present on a post. As of version 2.2.0, this behavior can be modified. The sample code snippet below will work just fine:

```php
/**
 * Override the early return if no subtitle exists.
 *
 * @see function is_archive
 * @see function in_the_loop
 */
function subtitle_does_exist() {
	return true;

} // end function subtitle_does_exist
add_filter( 'subtitle_exists', 'subtitle_does_exist' );
```

---

### Filtering All Subtitle Output ###

If you'd like to change the output of all subtitles throughout your site, use a function hooked to `the_subtitle`, for example:

```php
function better_subtitle( $title ) {
	return $title . 'Hello World';
}
add_filter( 'the_subtitle', 'better_subtitle' );
```

This will filter both the title and subtitle output after _Subtitles_ has done all of its magic.

---

### Using Template Tags ###

I very much hope that you do not need to use these template tags, because all of the above methods for handling subtitles should be enough. That said, in the event that you do need to use either `the_subtitle()` or `get_the_subtitle()`, they exist in the plugin and will give you a little bit more flexibility over your theme.

They work in the same way that `the_title()` and `get_the_title()` work, for example:

```php
if ( function_exists( 'the_subtitle' ) ) {
	the_subtitle( '<p class="entry-subtitle">', '</p>' );
}
```

Here's how using `get_the_subtitle` would look:

```php
if ( function_exists( 'get_the_subtitle' ) ) {
	echo get_the_subtitle( 35 );
}
```

An ID isn't necessary for `get_the_subtitle`, but will work for retrieving subtitles from posts that aren't currently being viewed.

---

### Modifying Allowed Tags ###

By default _Subtitles_ supports both bold and italicized text. If you want more control over this, you can take advantage of the `subtitles_allowed_tags` filter.

```php
function subtitles_mod_allowed_tags( $args ) {
	$args = array(
		'i' => array(), // italicized text
		'em' => array(), // emphasized text
		'strong' => array(), // strong text
		'a' => array(
			'href' => true, // links
		),
	);

	return $args;
} // end function subtitles_mod_allowed_tags
add_filter( 'subtitles_allowed_tags', 'subtitles_mod_allowed_tags' );
```
Proceed with caution here. In some cases getting too cavalier with this may introduce HTML issues into your site.

---

## Changelog

All versions of _Subtitles_ can be found on the [Releases](https://github.com/wecobble/Subtitles/releases) page.

### [v4.0.0] (TBD)

- TBD

### [v3.0.0](https://github.com/wecobble/Subtitles/releases/tag/v3.0.0) (August 8th, 2017)

- **Version Bump:** Fix all WordPress Coding Standards errors and update Tested Up To version.
- **Patch:** Transfer ownership of plugin to [We Cobble](https://wecobble.com/)
- **Patch:** Change plugin donation link to point to We Cobble PayPal account.

### [v2.2.1](https://github.com/wecobble/Subtitles/releases/tag/v2.2.1) (June 13th, 2016)

- **Version Bump:** Fix wonky 2.2.0 release. No changes here; just a version bump to fix the last release package.

### [v2.2.0](https://github.com/wecobble/Subtitles/releases/tag/v2.2.0) (June 13th, 2016)

- **Extra:** Allow theme and plugin authors to override the early return if no subtitle exists (see [issue](https://github.com/wecobble/Subtitles/issues/79)).
- **Extra:** Automatically enable subtitles support for Jetpack Testimonials (see [issue](https://github.com/wecobble/Subtitles/issues/78)).
- **Patch:** Remove French language packs so that they are able to be directly pulled from WordPress.org (see [issue](https://wordpress.org/support/topic/french-translation-updated-3)).
- **Patch:** Change jetpack.me links to jetpack.com.
- **Patch:** Change plugin donation link to point to Professional Themes PayPal account.

### [v2.1.1](https://github.com/wecobble/Subtitles/releases/tag/v2.1.1) (December 9th, 2015)

- **Bug Fix:** Remove redundant htmlspecialchars from admin input (see [issue](https://github.com/wecobble/Subtitles/issues/66])).
- **Patch:** Transfer ownership of plugin to Professional Themes.
- **Patch:** Give developers the option to show subtitles in RSS feeds (see [issue](https://github.com/wecobble/Subtitles/issues/61)).
- **Extra:** Lithuanian (lt_LT) language packs added.

### [v2.1.0](https://github.com/wecobble/Subtitles/releases/tag/v2.1.0) (July 19th, 2015)

- **Extra:** Add a Subtitle column into the Posts and Pages admin screens.
- **Extra:** We have added in a way for developers to allow more tags in subtitles input.
- **Extra:** Update plugin POT.
- **Patch:** Remove font sizing from hidden entry subtitle in comments area (see [issue](https://github.com/wecobble/Subtitles/issues/46])).

### [v2.0.1](https://github.com/wecobble/Subtitles/releases/tag/v2.0.1) (November 6th, 2014)

- **Bug Fix:** Do not show subtitles in RSS feeds (see [issue](https://github.com/wecobble/Subtitles/issues/32)).
- **Extra:** Russian (ru_RU) language packs added
- **Extra:** Better WordPress Coding Standards
- **Extra:** WordPress 4.1 introduced a new hook called `edit_form_before_permalink` that allows us to move Subtitles into a more natural position, just underneath the post title. Let's use that and preserve backwards compatibility for older versions of WordPress (see [issue](https://github.com/wecobble/Subtitles/issues/30)).

### [v2.0.0](https://github.com/wecobble/Subtitles/releases/tag/v2.0.0) (August 31st, 2014)

- **Performance Fix:** Better CSS Handling for better overall plugin performance (see [issue](https://github.com/wecobble/Subtitles/issues/28)).

### [v1.0.7](https://github.com/wecobble/Subtitles/releases/tag/v1.0.7) (August 17th, 2014)

- **Bug Fix:** Better backend tabbing from the title to the subtitle input field (see [issue](https://github.com/wecobble/Subtitles/issues/23)).
- **Extra:** Add default support for Jetpack Portfolios (see [issue](https://github.com/wecobble/Subtitles/issues/26)).

### [v1.0.6](https://github.com/wecobble/Subtitles/releases/tag/v1.0.6) (August 4th, 2014)

- **Bug Fix:** Better visual styling in the back end to keep up with WordPress 4.0

### [v1.0.5](https://github.com/wecobble/Subtitles/releases/tag/v1.0.5) (July 7th, 2014)

- **Bug Fix:** If subtitles are shown in comment areas, we'll hide them by default.
- **Bug Fix:** Better security for nonce checking after update to the WordPress VIP Coding Standards. See [this discussion](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards/issues/190) for more information.
- **Extra:** Wrap primary entry title parts in spans that theme authors can take advantage of for more fine-grained styling when a post has a subtitle.
- **Extra:** French (fr_FR) language packs added (see [issue](https://github.com/wecobble/Subtitles/pull/18)).

### [v1.0.4](https://github.com/wecobble/Subtitles/releases/tag/v1.0.4) (June 20th, 2014)

- **Bug Fix:** Make sure that other plugins that try to mess with titles do not cause _Subtitles_ to throw PHP warnings due to the second optional `$id` parameter not being sent to the primary `the_subtitles` method used throughout sites (see [issue](https://github.com/wecobble/Subtitles/issues/16)).

### [v1.0.3](https://github.com/wecobble/Subtitles/releases/tag/v1.0.3) (June 19th, 2014)

- **Bug Fix:** Ensure that _Subtitles_ works in PHP 5.2.4 environments (see [issue](https://github.com/wecobble/Subtitles/issues/8)).

### [v1.0.2](https://github.com/wecobble/Subtitles/releases/tag/v1.0.2) (June 18th, 2014)

- **Bug Fix:** Check if `$post` is set before proceeding with any title filtering for subtitles (see [issue](https://github.com/wecobble/Subtitles/issues/12)).
- **Bug Fix:** Add a single space between titles and subtitles so that they look sensible when being output as a title attribute (see [commit](https://github.com/wecobble/Subtitles/commit/5b54263fcf82de6db9e7e0875a0a99974758a81f)).
- **Extra:** Catalan (ca) language packs added (see [issue](https://github.com/wecobble/Subtitles/pull/11)).
- **Extra:** Korean (ko_KR) language packs added (see [issue](https://github.com/wecobble/Subtitles/pull/10)).
- **Extra:** Spanish (es_ES) language packs added (see [issue](https://github.com/wecobble/Subtitles/pull/11)).
- **Extra:** Begin preparing plugin for better automated testing via [Travis CI](https://travis-ci.org/), [phpunit](https://github.com/sebastianbergmann/phpunit/), [WordPress Coding Standards](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards), and [CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/)

### [v1.0.1](https://github.com/wecobble/Subtitles/releases/tag/v1.0.1) (June 14th, 2014)

- **Bug Fix:** Make sure that the plugin automatically works with `single_post_title` (see [issue](https://github.com/wecobble/Subtitles/issues/2)).
- **Bug Fix:** Ensure that special characters in post titles do not erroneously cause subtitles to be skipped during title filtering and checks (see [issue](https://github.com/wecobble/Subtitles/issues/3)).
- **Bug Fix:** Remove unnecessary ID checks against nav menus (see [issue](https://github.com/wecobble/Subtitles/issues/4)).
- **Bug Fix:** Resolve title output issues when [WordPress SEO by Yoast](https://wordpress.org/plugins/wordpress-seo/) breadcrumbs are used inside of [The Loop](http://codex.wordpress.org/The_Loop) (see [issue](https://github.com/wecobble/Subtitles/issues/5)).
- **Extra:** Vietnamese (vi_VN) language packs added.
- **Extra:** German (de_DE) language packs added.
- **Extra:** Finnish (fi) language packs added.
- **Extra:** Italian (it_IT) language packs added.
- **Extra:** Japanese (ja) language packs added.

### [v1.0.0](https://github.com/wecobble/Subtitles/releases/tag/v1.0.0) (June 12th, 2014)
- **Initial Release:** ([Launch Announcement](https://philip.blog/2014/06/12/subtitles/))

## Screenshots

Two primary screenshots have been shown in this README.md file, one of the post screen and one of an example of what subtitles will look like on the front end of your website. The [assets folder](https://github.com/wecobble/Subtitles/tree/master/assets) in this GitHub repository will be used to populate screenshots on the WordPress.org plugin site, and will not be included in the official plugin download from WordPress.org.

## Translations

See the [languages](https://github.com/wecobble/Subtitles/tree/master/languages) folder for more information on using _Subtitles_ in your language. These are considered "Extras" and will usually be released when a version bump has happened to _Subtitles_, for example during a bug fix or enhancement round of updates.

## Versioning

We've done our best to adhere to [Semantic Versioning](http://semver.org) for _Subtitles_.

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes,
2. MINOR version when you add functionality in a backwards-compatible manner, and
3. PATCH version when you make backwards-compatible bug fixes.

Most of the updates for this plugin will be in the form of bug fixes and minor enhancements.

## Build Status

Most commits and pull requests will undergo automatic build testing via [Travis CI](http://travis-ci.org/). The build result for the most recent non-skipped commit for master is at the top of this README.
