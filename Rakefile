require 'csv'
require 'rexml/document'

namespace :regenerate do
  task :all do
    # Parse source data files
    Dir.glob(File.join("*", "*.cat"), base: "source_data").each do |file|
      # Make the right directory
      Dir.mkdir(File.dirname(file)) unless Dir.exist?(File.dirname(file))
      # Write a CSV file
      CSV.open(file.gsub(".cat", ".csv"), "wb") do |csv|
        csv << ["model", "base_size", "base_short_axis", "base_shape", "notes"]
        File.open(File.join("source_data", file)) do |bsdata|
          xml = REXML::Document.new(bsdata)
          REXML::XPath.each(xml, "//*[@type='model']/@name") do |name|
            csv << [name, nil, nil, "unknown", nil]
          end
        end
      end
    end
  end
end