# Nokogiri for HTML Parsing in Ruby

Nokogiri is a powerful Ruby gem for parsing HTML and XML documents. It provides an easy-to-use interface for navigating and manipulating parsed content using CSS selectors or XPath expressions.

## Installation

First, install the gem:

```ruby
gem install nokogiri
```

## Basic Usage

```ruby
require 'nokogiri'
require 'open-uri'

# Parse from a string
html_string = "<html><body><h1>Hello World</h1></body></html>"
doc = Nokogiri::HTML(html_string)

# Parse from a file
doc = Nokogiri::HTML(File.open("index.html"))

# Parse from a URL
doc = Nokogiri::HTML(URI.open('https://example.com'))
```

## Finding Elements

### CSS Selectors
```ruby
# Find all paragraph tags
doc.css('p')

# Find elements with class "header"
doc.css('.header')

# Find elements with id "main"
doc.css('#main')

# Find nested elements
doc.css('div.content p.intro')
```

### XPath
```ruby
# Find all links
doc.xpath('//a')
```

## Working with Elements

```ruby
# Get the first matching element
first_paragraph = doc.at_css('p')

# Get element text
first_paragraph.text

# Get element HTML content
first_paragraph.inner_html

# Get attribute value
link = doc.at_css('a')
link['href'] # Gets the href attribute

# Iterate through all links
doc.css('a').each do |link|
  puts link['href']
end
```

## Modifying Documents

```ruby
# Add a class to an element
element = doc.at_css('#main')
element['class'] = 'highlighted'

# Create new elements
new_node = Nokogiri::HTML::Node.new('div', doc)
new_node.content = "New content"
doc.at_css('body').add_child(new_node)

# Remove elements
doc.css('.ads').remove
```

## Searching Within Context

```ruby
# Limit search to a specific part of the document
footer = doc.at_css('footer')
footer_links = footer.css('a') # Only finds links within footer
```

## Advanced Selectors

```ruby
# Select direct children only
doc.css('body > div')

# Select odd/even rows (useful for tables)
doc.css('table tr:nth-child(odd)')

# Select elements that have a specific attribute
doc.css('input[type="text"]')

# Select elements where attribute starts with a value
doc.css('a[href^="https"]')
```

## Handling Errors

```ruby
begin
  doc = Nokogiri::HTML(URI.open('https://invalid.url'))
rescue StandardError => e
  puts "Failed to parse: #{e.message}"
end
```

## Example: Scraping a Website

```ruby
require 'nokogiri'
require 'open-uri'

url = 'https://news.ycombinator.com/'
doc = Nokogiri::HTML(URI.open(url))

# Extract all story titles and links
doc.css('a.titlelink').each do |link|
  puts link.text
  puts link['href']
  puts "\n"
end
```

Enjoy parsing HTML with Nokogiri in Ruby! Let me know if you'd like any more specific examples or have questions about certain features.