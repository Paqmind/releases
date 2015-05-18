# Release questions

## Build folders and VCS

At least three different, mutually exclusive approaches may be defined here. 
Consequences of the suitable / unsuitable approach for your team are of critical importance
as one approach can't be easily switched to another.

### Approaches

#### Commit-bound
Builds are under VCS.
Every commit must include corresponding build changes (if there are).

#### Release-bound
Builds are under VCS.
Every release must include corresponding build changes.

#### Unbound 
Builds are out of VCS.
Fetches and builds are performed as part of install / update process.

<table>
<tr>
  <th>Negative Aspects</th>
  <th><h4>Commit-bound</h4></th>
  <th><h4>Release-bound</h4></th>
  <th><h4>Unbound</h4></th>
</tr>

<tr>
  <th>&nbsp;</th>
  <th colspan="3">Development</th>
</tr>  
<tr>
  <td>Diffs are huge / messy</td>
  <td><strong>yes</strong></td>
  <td>kinda</td>
  <td>no</td>
</tr>  
<tr>
  <td>Conflicts in minimized files</td>
  <td><strong>common</strong></td>
  <td>possible</td>
  <td>impossible</td>
</tr>
<tr>  
  <td>All team members must install dev. tools</td>
  <td>no</td>
  <td>maybe</td>
  <td><strong>yes</strong></td>
</tr>  
<tr>
  <td colspan="4"></td>
</tr>  

<tr>
  <th>&nbsp;</th><th colspan="3">Deployment</th>
</tr>  
<tr>
  <td>Is complicated</td>
  <td>no</td>
  <td>no</td>
  <td><strong>yes</strong></td>
</tr>  
<tr>
  <td>May break by network disconnect</td>
  <td>no</td>
  <td>no</td>
  <td><strong>yes</strong></td>
</tr>  
<tr>
  <td>May break by dep. repo removal</td>
  <td>no</td><td>no</td>
  <td><strong>yes</strong></td>
</tr>  
<tr>
  <td>Is slow</td>
  <td>no</td>
  <td>no</td>
  <td><strong>yes</strong></td>
</tr>  
<tr>
  <td>Untested dependency</td>
  <td>impossible</td>
  <td>possible in staging</td>
  <td><strong>possible in production</strong> (*)</td>
</tr>
<tr>
  <td>Sources and builds are unsynced</td>
  <td><strong>high probability</strong></td>
  <td>low probability</td>
  <td>zero probability</td>
</tr>
<tr>
  <td>Incompatible binaries</td>
  <td><strong>possible</strong></td>
  <td><strong>possible</strong></td>
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
  <th>&nbsp;</th><th colspan="3">Machine</th>
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

(*) – unsyncs between tested and installed dependency version may be
prevented to some degree by strict version pinning. Question about deps of deps remains.
Solution to is called "shrinkwrapping". Refer to corresponding tool suppport:
[Bower](https://github.com/bower/bower/pull/1592), [NPM](https://docs.npmjs.com/cli/shrinkwrap)
But even this don't give 100% guarantee when deps include binary stuff.

### Conclusion
All projects may be roughly divided into apps and libs.

It's quite clear that the **Commit-bound** approach is the worst by the **Development** and **History** aspect groups.
The **Unbound** approach has the opposite benefits and the worst **Deployment** metrics. The **Release-bound** sits somewhere in-between.

So what's to choose when? At this moment we believe that **Unbound** approach is the best one for apps. 
It makes development much easier in favor of complicated deployment, but this complication can be solved once and used forever. Tinier history is also more critical to apps, as their commit number is usually bigger in order(s) of magnitude.

It's very uncommon to run build step for libraries manually, so we use **Release-bound** approach for them.
We never use **Commit-bound** due to it's super-large history and overcomplicated development, especially when `build` includes 3-rd party libs (e.g. *always*).



