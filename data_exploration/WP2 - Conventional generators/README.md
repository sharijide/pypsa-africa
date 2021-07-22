# How to use `powerplantmatching`

The notebook in this directory show how to merge a few different databases of powerplants using the `powerplantmatching` tool.
However, the tool needs some setting up, which is further complicated by the fact that we have to use a fork of the tool with a few changes to accommodate for our model.

We use a fork of `powerplantmatching` at <https://github.com/koen-vg/powerplantmatching/tree/pypsa-africa> (the `pypsa-africa` branch, not `master`), included here is a git submodule.
To initialise the git submodule, got to the `powerplantmatching` directory and run `git submodule update --init`.

To install our local version of `powerplantmatching` into the conda `pypsa-africa` environment, run `pip install -e .` in the `powerplantmatching` directory.

Now it should be possible to build the powerplant database by running
```python
import powerplantmatching as pm
pm.powerplants(stored=False, update_all=True)
```
This uses a custom configuration for PyPSA-Africa at <https://github.com/koen-vg/powerplantmatching/blob/pypsa-africa/powerplantmatching/package_data/custom.yaml>, and stores the resulting database on your local machine (see `powerplantmatching` documentation at <https://powerplantmatching.readthedocs.io/en/latest/>.
Subsequent calls to `pm.powerplants()` will use the newly generated cached database and be fast.

## Changes to `powerplantmatching`

The `powerplantmatching` tool has been patched to work with two-letter country codes, since different databases use different names for countries.
We should consider offering this to upsteam (maybe making it configurable).
There are also some issues with using a custom configuration file for `powerplantmatching` (see <https://github.com/FRESNA/powerplantmatching/issues/41>), which is why for now we include our configuration directly into the `powerplantmatching` source code.
This should be changed once `powerplantmatching` is fixed to accept custom configs via the `pm.powerplants(config=<path>)` option.
