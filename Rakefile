require "bundler/gem_tasks"


desc 'Copy emoji static files to all of their aliased and unicode aliased locations'
task :deploy do
  require 'gemoji'

  target = "#{Rake.original_dir}/emoji"

  `mkdir -p #{target}`

  copy = lambda do |emoji, image_alias|
    `cp #{File.join(Emoji.images_path, 'emoji', emoji.image_filename)} #{File.join(target, "#{image_alias}.png")}`
  end

  payload = {}

  Emoji.all.each do |emoji|
    emoji.aliases.each do |image_alias|
      payload[image_alias] = "#{emoji.name}.png"
      copy.call(emoji, image_alias)
    end

    emoji.unicode_aliases.each do |image_alias|
      payload[image_alias] = "#{emoji.name}.png"
      copy.call(emoji, image_alias)
    end
  end

  f = File.new('image_paths.json', 'w+')
  f.write payload.to_json
  f.close
end
