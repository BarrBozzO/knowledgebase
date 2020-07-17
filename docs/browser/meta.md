# Meta

`<meta>` тэг определяет мета-данные о HTML документе. Мета-данные - это данные о данных.

`<meta>` тэги всегда идут внутри `<head>` элемента. Обычно используются для настройки набора символов(specify character set), описания страницы, ключевых слов (keywords), автора документа и настройки `viewport`.

Мета-данные не будут отображены на странице, но будут обработаны роботами.

Мета-данные используются браузом, поисковыми системами и другими веб-сервисами.

```
<meta name="keywords" content="HTML, CSS, JavaScript">
```

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

В зависимости от установленных атрибутов, тип метаданных может быть одним из следующих:

- Если в наборе `name`, то это document-level metadata, применяемая ко всей странице.
- Если в наборе `http-equiv`, то это _pragma directive_, то есть информация, веб-сервер предоставляет информацию о том, как должна обслуживаться веб-страница.
- Если в наборе `charset`, то это `charset declaration`, то есть кодировка, используемая для сериализованной формы веб-страницы.
- Если в наборе `itemprop`, то это user-defined metadata, прозрачна для агента пользователя, поскольку семантика метаданных зависит от пользователя

## Viewport

The viewport is the user's visible area of a web page. It varies with the device - it will be smaller on a mobile phone than on a computer screen.

You should include the following <meta> element in all your web pages:

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

This gives the browser instructions on how to control the page's dimensions and scaling.

The width=device-width part sets the width of the page to follow the screen-width of the device (which will vary depending on the device).

The initial-scale=1.0 part sets the initial zoom level when the page is first loaded by the browser.

Here is an example of a web page without the viewport meta tag, and the same web page with the viewport meta tag:

## Social Media

### Open Graph

Facebook uses OG

```
<meta property="og:title" content="European Travel Destinations">
<meta property="og:description" content="Offering tour packages for individuals or groups.">
<meta property="og:image" content="http://euro-travel-example.com/thumbnail.jpg">
<meta property="og:url" content="http://euro-travel-example.com/index.htm">
```

[Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/sharing/)

### Twitter

```
<meta name="twitter:title" content="European Travel Destinations ">
<meta name="twitter:description" content=" Offering tour packages for individuals or groups.">
<meta name="twitter:image" content=" http://euro-travel-example.com/thumbnail.jpg">
<meta name="twitter:card" content="summary_large_image">
```

[Twitter Card Validator](https://cards-dev.twitter.com/validator)

|             |                                                                                      Facebook                                                                                       |                                                                                                                                                    Twitter                                                                                                                                                     |
| ----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Title       |                                                                     The title, headline or name of the object.                                                                      |                                                                                                                       A concise title for the related content. [Maximum 70 characters.]                                                                                                                        |
| Description |                                                     A short description or summary of the object. [Between 2 and 4 sentences.]                                                      |                          A description that concisely summarizes the content as appropriate for presentation within a Tweet. You should not re-use the title as the description or use this field to describe the general services provided by the website. [Maximum 200 characters.]                          |
| Image       | The URL of the image for your object. It should be at least 600×315 pixels, but 1200×630 or larger is preferred (up to 5MB). Stay close to a 1.91:1 aspect ratio to avoid cropping. | A URL to a unique image representing the content of the page. You should not use a generic image such as your website logo, author photo, or other image that spans multiple pages. Images for this Card should be at least 280px in width, and at least 150px in height. Image must be less than 1MB in size. |
| URL         |                      The canonical URL for your page. This should be the undecorated URL, without session variables, user identifying parameters, or counters.                      |                                                                                                                                                                                                                                                                                                                |

## Джентельменский набор

[полезные-метатеги](https://canonium.com/articles/html-meta-tags/)

---

# References

[полезные-метатеги](https://canonium.com/articles/html-meta-tags/)
[w3-meta-tags](https://www.w3schools.com/tags/tag_meta.asp)
[meta-tags](https://metatags.io/)
[meta-tags-social-media](https://css-tricks.com/essential-meta-tags-social-media/)
[Open Graph protocol](https://ogp.me/)
[Основные мета-теги для социальных сетей](https://frontend-stuff.com/blog/meta-tags/)
[Set the viewport](https://web.dev/responsive-web-design-basics/#set-the-viewport)
