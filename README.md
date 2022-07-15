## BIG-IP Automation Toolchain InSpec Profile

This InSpec profile evaluates the following:
- basic connectivity to a BIG-IP management endpoint ('bigip-connectivity')
- availability of the Declarative Onboarding (DO) service ('bigip-declarative-onboarding')
- version reported by the Declarative Onboarding (DO) service ('bigip-declarative-onboarding-version')
- availability of the Application Services (AS3) service ('bigip-application-services')
- version reported by the Application Services (AS3) service ('bigip-application-services-version')
- availability of the Telemetry Streaming (TS) service ('bigip-telemetry-streaming')
- version reported by the Telemetry Streaming (TS) service ('bigip-telemetry-streaming-version')
- availability of the F5 Application Services Templates (FAST) service ('bigip-fast')
- version reported by the F5 Application Services Templates (FAST) service ('bigip-fast-version')
- availability of a license on the BIG-IP ('bigip-licensed')

In order to reference the profile you can include it as a dependency in your *inspec.yml* file
```yaml
depends:
  - name: big-ip-atc-ready
    git: https://github.com/F5SolutionsEngineering/big-ip-atc-ready
    branch:  master
```
and indicate which controls to use in your control ruby file
```ruby
# run all of the tests
require_controls 'big-ip-atc-ready' do
  control 'bigip-connectivity'
  control 'bigip-declarative-onboarding'
  control 'bigip-declarative-onboarding-version'
  control 'bigip-application-services'
  control 'bigip-application-services-version'
  control 'bigip-telemetry-streaming'
  control 'bigip-telemetry-streaming-version'
  control 'bigip-fast'
  control 'bigip-fast-version'
  control 'bigip-licensed'
end
```
```ruby
# run some of the tests
require_controls 'big-ip-atc-ready' do
  control 'bigip-connectivity'
  control 'bigip-declarative-onboarding'
  control 'bigip-licensed'
end
```

or you can call it at the command line
```bash
inspec exec https://github.com/f5devcentral/big-ip-atc-ready.git
```
Please refer to the [InSpec documentation](https://inspec.io) for more elaborate variants on these use cases and further use cases not documented here.

The profile requires a set of inputs which can be provided on the command line or with an input file. We listed the necessary inputs below in a sample YAML input file
```yaml
bigip_address: FQDN or ip address of the BIG-IP to test
bigip_port: the port for the BIG-IP management service, commonly 443
user: the user account with which to authenticate to the BIG-IP
password: the password to use to authenticate to the BIG-IP
do_version: the expected version of declarative onboarding
as3_version: the expected version of application services
ts_version: the expected version of telemetry streaming
```

Please refer to the [InSpec documentation for inputs](https://www.inspec.io/docs/reference/inputs/) for more detail
