require 'yaml'

namespace :translations do

  task :extract do
    translations = YAML.load_file('translation.yml')
    sentence_terminals = %w{. ! ? …}.to_set
    File.open('translation.txt', 'w') do |f|
      translations.each do |e|
        if e
          text = e[:Русский].strip
          next if text.empty?
          if sentence_terminals.include?(text[-1]) # some sentence
            text.concat ' '
          else # some header
            text.concat "\n"
          end
          f.write text
        else
          f.write "\n\n"
        end
      end
    end
  end

  task :check do
    translations = YAML.load_file('translation.yml')
    puts "Items: #{translations.size}"
    puts "Text items: #{translations.inject(0) { |a, e| e && !e[:Английский].strip.empty? ? a + 1 : a }}"
    puts "Translated items: #{translations.inject(0) { |a, e| e && !e[:Русский].strip.empty? ? a + 1 : a }}"
  end
end
