desc "Setup GitHub Pages Branch"
task :setup do
  io = IO.popen("git remote -v")
  log = io.readlines
  if log.any? {|line| line.match(/gh-pages/)}
    puts <<-DONE.gsub(/^ {6}/, '')
    Already setup!
    DONE
  else
    system "git checkout -b gh-pages > /dev/null && git checkout master > /dev/null"
    puts "Done."
  end
end

desc "Generate site and deploy to GitHub Pages"
task :deploy do
  puts "Generating site with Jekyll..."
  system "jekyll build"
  system "cp -rp _site/ ../tmp/"
  puts "Updating site locally..."
  system "git checkout gh-pages"
  system "rm -rf _includes"
  system "rm -rf _layouts"
  system "rm -rf _posts"
  system "rm -rf _site"
  system "rm -rf css"
  system "rm -rf font"
  system "rm -rf js"
  system "rm -rf jekyll"
  system "rm .gitignore"
  system "rm _config.yml"
  system "rm CNAME"
  system "rm index.md"
  system "rm Rakefile"
  system "rm index.html"
  system "cp -r ../tmp/ ./"
  system "rm -rf ../tmp"
  puts "Deploying..."
  system "git add --all > /dev/null && git commit -m 'Update site' > /dev/null && git push origin gh-pages > /dev/null"
  system "git checkout master"
  puts "Done."
end