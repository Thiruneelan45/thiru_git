# thiru_scraping
 pip install scrapy
 cat > myspider.py <<EOF
import scrapy

class BlogSpider(scrapy.Spider):
    name = 'blogspider'
    start_urls =["https://github.com/Thiruneelan45/thiru_git/edit/main/README.md"]

    def parse(self, response):
        for title in response.css('.oxy-post-title'):
            yield {'title': title.css('::text').get()}

        for next_page in response.css('a.next'):
            yield response.follow(next_page, self.parse)
EOF
 scrapy runspider myspider.py
