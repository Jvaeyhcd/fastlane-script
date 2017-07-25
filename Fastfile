# Customise this file, documentation can be found here:
# https://github.com/fastlane/fastlane/tree/master/fastlane/docs
# All available actions: https://docs.fastlane.tools/actions
# can also be listed using the `fastlane actions` command

# Change the syntax highlighting to Ruby
# All lines starting with a # are ignored when running `fastlane`

# If you want to automatically update fastlane if a new version is available:
# update_fastlane

# This is the minimum version number required.
# Update this, if you use features of a newer version
fastlane_version "2.45.0"

default_platform :ios

#指定项目的scheme名称
scheme="Project"
#蒲公英api_key和user_key
api_key=""
user_key=""

platform :ios do
  before_all do
    # ENV["SLACK_URL"] = "https://hooks.slack.com/services/..."
    cocoapods

  end

  desc "Runs all the tests"
  lane :test do
    scan
  end

  desc "Submit a new Beta Build to Apple TestFlight"
  desc "This will also make sure the profile is up to date"
  lane :beta do
    # match(type: "appstore") # more information: https://codesigning.guide
    gym(scheme: "Project") # Build your app - more options available
    pilot

    # sh "your_script.sh"
    # You can also use other beta testing services here (run `fastlane actions`)
  end

  desc "Deploy a new version to the App Store"
  lane :release do
    # match(type: "appstore")
    # snapshot
    gym(scheme: "Project") # Build your app - more options available
    deliver(force: true)
    # frameit
  end

  lane :pgyer do

    #指定项目的scheme名称
    scheme="Project"
    #指定要打包的配置名
    configuration="Adhoc"
    #指定打包所使用的输出方式，目前支持app-store, package, ad-hoc, enterprise, development, 和developer-id，即xcodebuild的method参数
    export_method="ad-hoc"

    #指定项目地址
    workspace_path="Project.xcworkspace"
    #指定输出路径
    output_path="/Users/Jvaeyhcd/Desktop/"
    #指定输出归档文件地址
    archive_path="$output_path/Project_${now}.xcarchive"
    #指定输出ipa地址
    ipa_path="$output_path/Project_${now}.ipa"
    #指定输出ipa名称
    ipa_name="Project_${now}.ipa"

    gym(
      workspace: workspace_path,
      scheme: scheme,
      clean: true,
      configuration: configuration,
      export_method: export_method,
      include_bitcode: true,
      include_symbols: false,
      archive_path: archive_path,
      output_directory: output_path,
      output_name: ipa_name
    )

    puts "开始上传蒲公英"
    # 开始上传蒲公英
    pgyer(api_key: api_key, user_key: user_key)
  end

  # You can define as many lanes as you want

  after_all do |lane|
    # This block is called, only if the executed lane was successful

    # slack(
    #   message: "Successfully deployed new App Update."
    # )
  end

  error do |lane, exception|
    # slack(
    #   message: exception.message,
    #   success: false
    # )
  end
end


# More information about multiple platforms in fastlane: https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Platforms.md
# All available actions: https://docs.fastlane.tools/actions

# fastlane reports which actions are used. No personal data is recorded.
# Learn more at https://github.com/fastlane/fastlane#metrics
