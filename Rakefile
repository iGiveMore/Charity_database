require 'net/http'
require 'zip/zip'

states = ["ak", "al", "ar", "az", "ca", "co", "ct", "dc", "de", "fl", "ga", 
          "hi", "ia", "id", "il", "in", "ks", "ky", "la", "ma", "md", "me", 
          "mi", "mn", "mo", "ms", "mt", "nc", "nd", "ne", "nh", "nj", "nm", 
          "nv", "ny", "oh", "ok", "or", "pa", "pr", "ri", "sc", "sd", "tn", 
          "tx", "ut", "va", "vt", "wa", "wi", "wv", "wy", "xx"]

def download_state(state)
  puts "\n\n-- Downloading Zip file for #{state}"
  Net::HTTP.start("www.irs.gov") do |http|
    resp = http.get("/pub/irs-soi/eo_#{state}.zip")
    open(File.join(Dir.pwd, "zips", "#{state}.zip"), "wb") { |file| file.write(resp.body) }
  end
end

def unzip_file (file, destination)
  puts "-- Unziping #{file} to #{destination}"
  Zip::ZipFile.open(file) { |zip_file|
   zip_file.each { |f|
     f_path=File.join(destination, f.name)
     FileUtils.mkdir_p(File.dirname(f_path))
     zip_file.extract(f, f_path) unless File.exist?(f_path)
   }
  }
end
         
namespace :igivemore do
  namespace :tax_status do
    task :seed do
      states.each do |state|
        download_state state
        unzip_file File.join(Dir.pwd, "zips", "#{state}.zip"), File.join(Dir.pwd, "extracted", "#{state}")
      end
    end
  end
end