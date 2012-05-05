require 'rake'

def _pdf(lang = :es)
  tex_file = "cv_#{lang}.tex"

  $stdout.puts "Generating the pdf file for: #{tex_file}"
  system %Q(xelatex #{tex_file})
end

def _languages
  [:es, :en]
end

def _packages
  [
    "fontspec",
    "geometry",
    "color",
    "xunicode",
    "xltxtra",
    "marginnote",
    "sectsty",
    "ulem",
    "hyperref",
  ]
end

namespace :pdf do
  _languages.each do |lang|
    desc "Create pdf file for #{lang}."
    task lang do
      _pdf(lang)
    end
  end
end

desc "Remove LaTeX temporal files."
task :clean do
  system %Q(rm -f *.{aux,log,out})
end

desc "Setup some missing packages for LaTeX."
task :setup do
  _packages.each do |package|
    $stdout.puts "Installing LaTeX package: #{package}"
    system %Q(tlmgr install #{package})
  end
end

task :pdf => _languages.map { |t| "pdf:#{t}" } + ["clean"]
task :default => :pdf
