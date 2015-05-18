# Release questions

## Build folders and VCS

At least 3 well-defined approaches to this may be established. All have their own benefits
and drawbacks and require entirely mutuall exclusive decisions in a lot of cases.
So it's better to completely understand consequences of the choice for your team.

### Options

#### Full
Builds are under VCS.
Every commit must include corresponding build changes (if there are).

#### Partial 
Builds are under VCS.
Every release must include corresponding build changes.

#### Pure 
Builds are out of VCS.
Fetches and builds are performed as part of install / update process.

<table>
<tr>
  <th>Negative Aspects</th><th><h4>Full</h4></th><th><h4>Partial</h4></th><th><h4>Pure</h4></th>
</tr>

<tr>
  <th>&nbsp;</th><th colspan="3">Development</th>
</tr>  
<tr>
  <td><code>$ git add -p</code> is complicated</td><td><strong>yes</strong></td><td>kinda</td><td>no</td>
</tr>  
<tr>  
  <td>Every member must have dev. tools installed</td><td>no</td><td>maybe</td><td><strong>yes</strong></td>
</tr>  
<tr>
  <td colspan="4"></td>
</tr>  

<tr>
  <th>&nbsp;</th><th colspan="3">Deployment</th>
</tr>  
<tr>
  <td>Is complicated</td><td>no</td><td>no</td><td><strong>yes</strong></td>
</tr>  
<tr>
  <td>May break by network disconnect</td><td>no</td><td>no</td><td><strong>yes</strong></td>
</tr>  
<tr>
  <td>May break by dep. repo removal</td><td>no</td><td>no</td><td><strong>yes</strong></td>
</tr>  
<tr>
  <td>Is slow</td><td>no</td><td>no</td><td><strong>yes</strong></td>
</tr>  
<tr>
  <td colspan="4"></td>
</tr>  

<tr>
  <th>&nbsp;</th><th colspan="3">Commits</th>
</tr>  
<tr>
  <td>Sources and dists are unsynced</td>
  <td><strong>high probability</strong></td>
  <td>low probability</td>
  <td>zero probability</td>
</tr>
<tr>
  <td>Untested dependency</td>
  <td>impossible</td>
  <td>possible in staging</td>
  <td><strong>possible in production</strong> (*)</td>
</tr>
<tr>
  <td>Incompatible binaries</td>
  <td><strong>possible</strong></td>
  <td><strong>possible</strong></td>
  <td>impossible</td>
</tr>
<tr>
  <td>Conflicts in minimized files/td>
  <td><strong>common</strong></td>
  <td>possible</td>
  <td>impossible</td>
</tr>
<tr>
  <td colspan="4"></td>
</tr>

<tr>
  <th>&nbsp;</th><th colspan="3">Tags / versions</th>
</tr>  
<tr>
  <td>Are locked</td><td>no</td><td><strong>yes</strong></td><td>no</td>
</tr>
<tr>
  <td colspan="4"></td>
</tr>

<tr>
  <th>&nbsp;</th><th colspan="3">History</th>
</tr> 
<tr>
  <td>Bigger commits</td><td><strong>yes</strong></td><td>kinda</td><td>no</td>
</tr>
<tr>
  <td>Bigger repo</td><td><strong>yes</strong></td><td><strong>yes</strong></td><td>no</td>
</tr>
<tr>
  <td colspan="4"></td>
</tr>
</table>

### Aspects

All projects may be roughly divided into apps and libs.

#### Development
Critical to both apps and libs.

#### Deployment
Critical to apps. Agnostic to libs.

#### Commits
Cricital to both apps and libs. Broken commits may cause multiple problems.
(*) – unsyncs between tested and installed dependency version may be
prevented to some degree by strict version pinning. Question about deps of deps remains.
Solution to is called "shrinkwrapping". Refer to corresponding tool suppport:
[Bower](https://github.com/bower/bower/pull/1592), [NPM](https://docs.npmjs.com/cli/shrinkwrap)
But even this don't give 100% guarantee when deps include binary stuff.

#### Tags / versions
Medium importance to both apps and libs.

#### History
Bigger history increases disk and traffic usage. Probably is more critical to apps
considering their commit number is usually bigger in order(s) of magnitude.
