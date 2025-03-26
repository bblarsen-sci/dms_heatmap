# dms_heatmap
Create 'wrapped' heatmaps from DMS data using [Altair](https://altair-viz.github.io). Notebook allows you to specify number of rows, color, stroke width, etc to customize visualization. 

**Note - Does not handle insertions or deletions in the data.**

An example of the output:

<img src="./results/e3_entry_heatmap.png">

## Download

To download the script, clone the repository using the following command:

```bash
git clone https://github.com/bblarsen-sci/dms_heatmap.git
```

## Usage

First, build the conda environment using the provided `environment.yml` file:

```bash
conda env create -f environment.yml
```

To use the script, modify the `workflow/notebooks/wrapped_heatmap.ipynb` notebook to load your data and specify the number of rows, color, stroke width, etc. 

```python
def main():
    # user parameters
    data_path = "../../data/e3_entry_filtered.csv" #filtered DMS data
    file_name_prefix = "e3_entry" #what you want the files to be called
    heatmap_rows = 6 #how many rows you want in the heatmap
    
    # run the analysis
    df = pd.read_csv(data_path).round(2)
    merged_df = make_empty_df(df)
    prepared_df = prepare_data(merged_df)
    wildtype_df = prepare_wt_data(prepared_df)
    min_val, max_val = find_min_max(prepared_df)
    full_ranges = create_full_ranges(min_val, max_val, heatmap_rows)

    plot = plot_heatmap(
        prepared_df, 
        wildtype_df,
        full_ranges,
        legend_title = 'CHO-bEFNB3 Entry',
        plot_title = 'CHO-bEFNB3 Entry',
        subtitle_str = 'Nipah RBP mutational effects on cell entry relative to the unmutated reference sequence',
        stroke_width = 1.5,
        stroke_color = 'white',
    )
    plot.save(f'../../results/{file_name_prefix}_heatmap.svg')
    plot.save(f'../../results/{file_name_prefix}_heatmap.png', ppi=200)
    plot.display()

if __name__ == "__main__":
    main()
```

Then run the notebook to generate the heatmap. 

The list of options for customizing appearance of the heatmap are here

```
Parameters
    ----------
    legend_title : str
        Title for the legend
    plot_title : str
        Title for the plot
    subtitle_str : str
        Subtitle for the plot
    stroke_width : float
        Width of the stroke for the effect chart
    stroke_color : str
        Color of the stroke for the effect chart
    effect_color_scheme : str
        Color scheme for the effect. Possible values are 'blueorange','brownbluegreen','purplegreen','pinkyellowgreen','purpleorange', 'redblue','redgrey','redyellowblue'
    domain : list
        List of two values for the domain of the color scale
    null_color : str
        Color for the mutants which have no associated DMS
```


