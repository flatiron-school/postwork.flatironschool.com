desc "Setup GitHub Pages Branch"
task :setup do
  io = IO.popen("git branch -v")
  log = io.readlines
  if log.any? {|line| line.match(/gh-pages/)}
    puts <<-DONE.gsub(/^ {6}/, '')
    Already setup!
    DONE
  else
    system "git checkout -b gh-pages --quiet && git checkout master --quiet"
    puts "Done."
  end
end

desc "Generate site and deploy to GitHub Pages"
task :deploy do
  puts "Generating site with Jekyll..."
  system "jekyll build > /dev/null"
  system "cp -rp _site/ ../tmp/"
  puts "Updating site locally..."
  system "git checkout gh-pages --quiet"
  system "rm -rf _includes > /dev/null"
  system "rm -rf _layouts > /dev/null"
  system "rm -rf _posts > /dev/null"
  system "rm -rf _site > /dev/null"
  system "rm -rf css > /dev/null"
  system "rm -rf font > /dev/null"
  system "rm -rf js > /dev/null"
  system "rm -rf jekyll > /dev/null"
  system "rm .gitignore > /dev/null"
  system "rm _config.yml > /dev/null"
  system "rm CNAME > /dev/null"
  system "rm index.md > /dev/null"
  system "rm Rakefile > /dev/null"
  system "rm index.html > /dev/null"
  system "cp -r ../tmp/ ./"
  system "rm -rf ../tmp > /dev/null"
  puts "Deploying..."
  system "git add --all && git commit -m 'Update site' --quiet && git push origin gh-pages --quiet"
  system "git checkout master --quiet"
  puts "Done."
end