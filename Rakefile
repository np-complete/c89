require 'review'
require 'rake/clean'

SRCS = FileList['*.md']
OBJS = SRCS.ext('re')
TARGET = 'c87.pdf'

CLEAN.include(OBJS)
CLOBBER.include(TARGET)

rule '.re' => '.md' do |t|
  sh "bundle exec md2review --render-link-in-footnote #{t.source} > #{t.name}"
end

desc "generate pdf"
file TARGET => OBJS + %w{catalog.yml config.yml locale.yml titlepage.tex}  do |t|
  rm_rf 'c87-pdf' if File.exist?('c87-pdf')
  rm TARGET if File.exist?(TARGET)
  sh "bundle exec review-pdfmaker config.yml"
end

task :default => TARGET
