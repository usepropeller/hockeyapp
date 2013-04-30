# HockeyApp gem

This gem enables you to easily access the JSON Rest API of http://www.hockeyapp.net.

More info available on this API here : http://support.hockeyapp.net/kb/api


## Usage

### Configure your connection

```ruby
HockeyApp::Config.configure do |config|
  config.token = "ABCDEF"
end
```

### Make a client

```ruby
client = HockeyApp.build_client
```

### Use the client

```ruby
apps = client.get_apps
versions = apps.first.versions
crashes = apps.first.crashes
```

## Documentation

### Uploading a new version

```ruby
@client ||= HockeyApp.build_client

app = HockeyApp::App.new(@client)
app.public_identifier = "aklsdjklajsd"
version = HockeyApp::Version.new(app, @client)
version.ipa = File.new('./app.ipa', 'r')
version.dsym = File.new('./dsym.dSYM.zip', 'r')
version = @client.post_new_version version
```