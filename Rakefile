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
  current_dir = Dir.pwd
  system 'git rev-parse && cd "$(git rev-parse --show-cdup)"'
  puts "Generating site with Jekyll..."
  system "jekyll build > /dev/null 2>&1"
  system "cp -rp _site/ ../tmp/"
  puts "Updating site locally..."
  system "git checkout gh-pages --quiet"
  system "rm -rf _includes > /dev/null 2>&1"
  system "rm -rf _layouts > /dev/null 2>&1"
  system "rm -rf _posts > /dev/null 2>&1"
  system "rm -rf _site > /dev/null 2>&1"
  system "rm -rf css > /dev/null 2>&1"
  system "rm -rf font > /dev/null 2>&1"
  system "rm -rf js > /dev/null 2>&1"
  system "rm -rf jekyll > /dev/null 2>&1"
  system "rm .gitignore > /dev/null 2>&1"
  system "rm _config.yml > /dev/null 2>&1"
  system "rm CNAME > /dev/null 2>&1"
  system "rm index.md > /dev/null 2>&1"
  system "rm Rakefile > /dev/null 2>&1"
  system "rm index.html > /dev/null 2>&1"
  system "cp -r ../tmp/ ./"
  system "rm -rf ../tmp > /dev/null 2>&1"
  puts "Deploying..."
  system "git add --all && git commit -m 'Update site' --quiet && git push origin gh-pages --quiet"
  system "git checkout master --quiet"
  system "cd #{current_dir}"
  puts "Done."
end