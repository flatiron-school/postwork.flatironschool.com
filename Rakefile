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
  system "jekyll build 2> /dev/null"
  system "cp -rp _site/ ../tmp/"
  puts "Updating site locally..."
  system "git checkout gh-pages --quiet"
  system "rm -rf _includes 2> /dev/null"
  system "rm -rf _layouts 2> /dev/null"
  system "rm -rf _posts 2> /dev/null"
  system "rm -rf _site 2> /dev/null"
  system "rm -rf css 2> /dev/null"
  system "rm -rf font 2> /dev/null"
  system "rm -rf js 2> /dev/null"
  system "rm -rf jekyll 2> /dev/null"
  system "rm .gitignore 2> /dev/null"
  system "rm _config.yml 2> /dev/null"
  system "rm CNAME 2> /dev/null"
  system "rm index.md 2> /dev/null"
  system "rm Rakefile 2> /dev/null"
  system "rm index.html 2> /dev/null"
  system "cp -r ../tmp/ ./"
  system "rm -rf ../tmp 2> /dev/null"
  puts "Deploying..."
  system "git add --all && git commit -m 'Update site' --quiet && git push origin gh-pages --quiet"
  system "git checkout master --quiet"
  puts "Done."
end