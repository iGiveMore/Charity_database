require 'net/http'

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
         
namespace :igivemore do
  namespace :tax_status do
    task :seed do
      states.each do |state|
        download_state state
      end
    end
  end
end