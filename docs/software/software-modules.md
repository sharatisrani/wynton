# Software Modules

In addition to the [core software] tools that are available by default, additional software is available via different [Software Repositories].  Note that some of these software tools are installed and maintained by other users or research groups of the cluster who have kindly agreed on sharing their efforts with other cluster users. Currently known and publicly shared repositories are:

<table>
<tr>
  <th>Repository</th>
  <th>Description</th>
 </tr>
 <tr>
  <td>
  <strong>CBI</strong><br>
  </td>
  <td>
  <strong>The Computational Biology and Informatics (CBI) Software Repository</strong><br>
  Repository of software shared by the Computational Biology and Informatics (<a href="http://cbi.ucsf.edu">http://cbi.ucsf.edu</a>) at the UCSF Helen Diller Family Comprehensive Cancer Center.<br>
  Usage: <code>module load CBI</code>
  </td>
 </tr>
 <tr>
  <td>
  <strong>Sali</strong><br>
  
  </td>
  <td>
  <strong>Sali Lab Software Repository</strong><br>
  Repository of software shared by the UCSF Sali Lab (<a href="https://salilab.org/">https://salilab.org/</a>).<br>
  <em>Comment: Contrary to the UCSF QB3 cluster, where these modules were available by default, this repository has to be loaded explicitly in order to have access to its modules on {{ site.cluster.name }} HPC.</em><br>
  
  Usage: <code>module load Sali</code>
  </td>
 </tr>
</table>
<br>

To get access to the software available in one or more of these repositories, load the repository using `module load <repos>` (on command line and in script).  After loading a software repository, all of its software tools are available as _environment modules_, that is, they can in turn be loaded using `module load <software>`.


## Example

The [R] software is available in software repository CBI.  To use that R installation, first make sure to enable ("load") the repository and then the software as in:
```sh
module load CBI   ## Enables the software repository
module load r     ## Enables R
```
or, shorter (order is important):
```sh
module load CBI r
```

After this, the `R` and the `Rscript` commands are available on the search path (`PATH`), e.g.
```sh
$ Rscript --version
R scripting front-end version 3.5.3 (2019-03-11)
```

<div class="alert alert-warning" role="alert">
<strong>For jobs, software modules need to be loaded in the submitted job script - </strong> it is <em>not</em> enough to load them in the terminal before submitting the job to the scheduler.
</div>

To disable ("unload") R, that is, remove it from the search path, do:
```sh
module unload r
```

<br>
<div class="alert alert-warning" role="alert">
If you unload a <em>repository</em>, any of its software modules that are loaded will be <em>deactivated</em> - they remain listed but act as they never have been loaded.  If you then reload the repository, such software modules will be activated again.
</div>

To see what software modules you have currently loaded, use:
```sh
module list
```
To disable all loaded software modules and repositories, use:
```sh
module purge
```

To see what software modules are currently available (in the software repositories you have loaded), use:
```sh
module avail
```
or alternative,
```sh
module spider
```

If the software repository provides more than one version of each software, specific versions can be loaded using the `module load <software>/<version>` format.  For instance, the CBI repository provides a large number of historical R versions.  To load R 3.2.0, use:
```sh
module load r/3.2.0
```
_Comment_: If another version of R is already loaded, that will automatically be unloaded before loading the new version.



<br>
<div class="alert alert-info" role="alert">
The names of software repositories are always capitilized (e.g. <code>CBI</code> and <code>Sali</code>) whereas the names of the software themselves are typically in all lower case (e.g. <code>r</code> and <code>bwa</code>).  This makes it easier to distiguish between repositories and software.
</div>


## See also

For more information on how to use modules and the `module` command, see `module --help`, `man module`, and the official [Lmod documentation].


## Technical details

Instead of the classical Tcl-based environment module system commonly available on Linux, the cluster uses a Lua-based environment module system called [Lmod].  Lmod has a several advantages over the Tcl-based module system while being backward compatible, i.e. users of Tcl modules can still use them with Lmod.  There are [a few rare corner cases](http://lmod.readthedocs.io/en/latest/095_tcl2lua.html) where a Tcl module might fail and the module has to be rewritten as a Lua-based module.

When loading a _software repository_ (`module load <repos>`), it will append its module folder to the `$MODULEPATH`.  Unloading it (`module unload <repos>`) will undo any changes.  For instance, `module load <repos>` appends `$MODULEPATH_ROOT/<repos>` to your `$MODULEPATH`.  Multiple software repositories can be loaded in one call, e.g. `module load <repos1> <repos2>`.  It is also possible to load a software repository and some of its software tools in one call, e.g. `module load <repos> <software1> <software2>`.


[core software]: {{ '/software/core-software.html' | relative_url }}
[R]: https://www.r-project.org
[Lmod]: https://github.com/TACC/Lmod
[Lmod documentation]: https://lmod.readthedocs.io/en/latest/
[Software Repositories]: {{ '/software/software-repositories.html' | relative_url }}
