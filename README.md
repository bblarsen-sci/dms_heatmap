# dms_heatmap
Create 'wrapped' heatmaps from DMS data using [Altair](https://altair-viz.github.io). Notebook allows you to specify number of rows, color, stroke width, etc to customize visualization. Does not handle insertions or deletions in the data. 

An example of the output:

<img src="./results/e2_entry_heatmap.png">

## Download

To download the script, clone the repository using the following command:

```bash
git clone https://github.com/bblarsen-sci/dms_heatmap.git
```

## Usage

To use the script, modify the `workflow/notebooks/wrapped_heatmap.ipynb` notebook to load your data and specify the number of rows, color, stroke width, etc. Then run the notebook to generate the heatmap. If needed, an `environment.yml` file is provided to create a conda environment with the necessary dependencies.


