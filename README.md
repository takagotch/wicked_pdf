### wicked_pdf
---
https://github.com/mileszs/wicked_pdf

```
gem 'wicked_pdf'
rails g wicked_pdf
Mime::Type.register "application/pdf", :pdf
gem 'wkhtmltopdf-binary'
bundle install
```

```ruby
WickedPdf.config = {
  exe_path: '/usr/local/bin/wkhtmlpdf'
}

class ThingsController < ApplicationController
  def show
    respond_to do |format|
      format.html
      format.pdf do
        render pdf: "file_name"
      end
    end
  end
end

config.assets.percompile += ['blueprint/screen.css', 'pdf.css', 'jqueery.ui.datapicker.js', 'pdf.js', ]

class ThingsController < ApplicationController
  def show
    respond_to do |format|
      format.html
      format.pdf do
        render pdf: 'filename',
               disposition: 'attachment',
               template: 'things/show',
               file: "#{Rails.root}/files/foo.erb"
               layout: 'pdf',
               wkhtmltopdf: '/usr/local/bin/whtmltopdf',
               show_as_html: params.key?('debug'),
               orientation: 'Landscape',
               page_size: ''A4, Letter, ... ,
               page_width: NUMBER,
               page_width: NUMBER,
               save_to_file: Rails.root.join('pdfs', "#{filename}.pdf"),
               save_only: false,
               default_protcol: 'http',
               proxy: 'TEXT',
               basic_auth: false
               username: 'TEXT',
               password: 'TEXT',
               title: 'Alternate Title',
               cover: 'URL, Pathname, or raw HTML string',
               dpi: 'dpi',
               encoding: 'TEXT',
               user_style_sheet: 'URL',
               cookie: ['_session_id_SESSION_ID'],
               post: ['query QUERY_PARAM'],
               redirect_delay: NUMBER,
               javascript_delay: NUMBER,
               window_status: 'TEXT',
               image_quality: NUMBER,
               no_pdf_compression: true,
               zoom: FLOAT,
               page_offset: NUMBER,
               book: true,
               default_header: true,
               disable_javascript: false,
               grayscale: true,
               lowquality: true,
               enable_plugins: true,
               disable_internal_links: true,
               disable_external_links: true,
               print_media_type: true,
               disable_smart_shrinking: true,
               use_xserver: true,
               background: false,
               no_background: true,
               viewport_size: 'TEXT',
               extra: '',
               raise_on_all_errors: nil,
               outline: { outline: true,
                          outline_depth: LEVEL },
               margin: { top: SIZE,
                         bottom: SIZE,
                         left: SIZE,
                         right: SIZE },
               headers: { html: { html: { template: 'users/header',
                                          layout: 'pdf_plain',
                                          url: 'www.example.com',
                                          locals: { foo: @bar }},
                          center: 'TEXT',
                          font_name: 'NAME',
                          left: 'TEXT',
                          right: 'TEXT',
                          spacing: REAL,
                          line: true,
                          content: 'HTML CONTENT ALREADY RENDERED'},
               footer: { html: { template:'shared/footer',
                                 layout: 'pdf_palin.html',
                                 url: 'www.example.com',
                                 locals: { foo: @bar }},
                         center: 'TEXT',
                         font_name: 'NAME',
                         font_size: SIZE,
                         left: 'TEXT',
                         right: 'TEXT',
                         spacing: REAL,
                         line: true,
                         content: 'HTML CONTENT ALREADY RENDERED'},
               toc: { font_name: "NAME",
                      depth: LEVEL,
                      headers_text: "",
                      text_size_shrink: 0.8,
                      l1_font_size: SIZE,
                      l2_font_size: SiZE,
                      l3_font_size: SIZE,
                      l4_font_size: SIZE,
                      l5_font_size: SIZE,
                      l6_font_size: SIZE,
                      l7_font_size: SIZE,
                      level_indentation: NUM,
                      l1_identation: NUM,
                      l2_identation: NUM,
                      l3_identation: NUM,
                      l4_identation: NUM,
                      l5_identation: NUM,
                      l6_identation: NUM,
                      l7_identation: NUM,
                      no_dots: true,
                      disable_dotted_lines: true,
                      disable_links: true,
                      disable_toc_links: true,
                      disable_back_links: true,
                      xsl_style_sheet: 'file.xsl'}
      end
    end
  end
end

print_media_type: true
no_background: true

pdf = WickedPdf.new.pdf_from_string'<h1>Hello</h1>')
pdf = WickedPdf.new.pdf_from_html_file('/your/absolute/path/here')
pdf = WickedPdf.new.pdf_from_url('https://github.com/mileszs/wicked_pdf')
pdf = WickedPdf.new.pdf_from_string(
  render_to_string('https://github.com/mileszs/wicked_pdf'),
  footer: {
    content: render_to_string(
      'templates/footer',
      layout: 'pdfs/layout_pdf.html'
    )
  }
)
pdf = WickedPdf.new.pdf_from_string(
  render_to_string('templates/full_header_template'),
  header: {
    content: render_to_string('templates/full_headers_template')
  }
)
pdf = render_to_string pdf: "some_file_name", template: "templates/pdf", encoding: "UTF-8"
save_path = Rails.root.join('pdfs', 'filename.pdf')
File.open(save_path, 'wb') do |file|
  file << pdf
end

render pdf: 'filename', header: { right: '[page] of [topage]' }

require 'wicked_pdf'
config.middleware.use WickedPdf::Middleware

config.middleware.use WickedPdf::Middleware, {}, only: '/invoice'
config.middleware.use WickedPdf::Middleware, {}, except: [ %r[^/admin], '', %r[^/people/\d] ]

attachments['attachment.pdf'] = WickedPdf.new.pdf_from_string(
  render_to_string('link_to_view.pdf.erb', layout: 'pdf')
)
```

```
<!doctype html>
<html>
  <head>
    <meta charset='utf-8' />
    <%= wicked_pdf_stylesheet_link_tag "pdf" %>
    <%= wicked_pdf_javascript_include_tag "number_pages" %>
  </head>
  <body onload='number_pages'>
    <div id="header">
      <%= wicked_pdf_image_tag 'mysite.jpg' %>
    </div>
    <div id="content">
      <%= yield %>
    </div>
  </body>
</html>

<!doctype html>
<html>
  <head>
    <meta charset='utf-8' />
    <%= stylesheet_link_tag wicked_pdf_asset_base64("pdf") %>
    <%= javascript_include_tag wicked_pdf_asset_base64("number_page") %>
  </head>
  <body onload='number_pages'>
    <div id="header">
      <%= image_tag wicked_pdf_asset_base64('mysite.jpg') %>
    </div>
    <div id="content">
      <%= yield %>
    </div>
  </body>
</html>

<!doctype html>
<html>
  <head>
    <%= javascript_include_tag "http://code.jquery.com/jquery-1.10.0.min.js" %>
    <%= javascript_include_tag "http://code.jquery.com/ui.1.10.3/jquery-ui.min.js" %>

<html>
  <head>
    <script>
      function number_page(){
        var vars={};
        var x=document.location.search.substring(`).split('&');
        for(var i in x){ var z=x[i].split();vars[] = decodeURIComponent(z[1]);}
        var x=['frompage', 'topage', 'page', 'webpage', 'section', 'subsection', 'sebsucsection'];
        for(var i in x){
          var y = document.getElementByClassName(x[i]);
          for(var j=0; j<y.length; ++j) y[j].textContent = vars[x[i]];
        }
      }
    </script>
  </head>
  <body onload="number_pages()">
    Page <span class="page"></span><span class="topage"></span>
  </body>
</html>

<%= params.key?('debug') ? image_tag('foo') : wicked_pdf_image_tag('foo') %>

<meta charset="utf-8"/>
```

```css
div.alwaysbreak { page-break-before: always; }
div.nobreak:before { clear:both; }
div.nobreak { page-break-inside: avoid; }
```


