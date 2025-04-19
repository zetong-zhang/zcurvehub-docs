# Quickstart
We provide the installation of the Python package here, along with a set of simple examples of its usage. Please read the tutorial of Web Service [here](./webserver.md) if you want to use the functions on the Internet.
## Installation
Python includes the package management system `pip` which should allow you to install ZCurvePy and its dependencies if needed, as well as upgrade or uninstall with just one command in the terminal:
```bash
python -m pip install zcurvepy
python -m pip install --upgrade zcurvepy

python -m pip uninstall zcurvepy
```
Starting from 1.5.11, the return value types of some frequently used API functions have been modified from Python list to Numpy ndarray. Therefore, please install Numpy 1.x before compiling and installing.
```bash
python -m pip install numpy>=1.21,<2.0
```
### Python Requirements
Python 3.7, 3.8, 3.9, 3.10 and 3.11 are supported. We currently recommend using Python 3.9.6 (https://www.python.org/downloads/release/python-396/)
### Operating System
Windows 10/11, macOS, and Linux running on x86_64 arch are supported. Note that some features of Matplotlib may not work on systems without a graphic interface (e.g., RedHat).
## Code Examples
1. Generate Z-curves and derivatives  
   (1) Python API implementation:  

    ```python
    from ZCurvePy import ZCurvePlotter
    from ZCurvePy.RunnableScriptsUtil import download_acc
    from Bio.SeqIO import read
    import matplotlib.pyplot as plt
    # Download genomes (Please wait for several seconds)
    save_paths = download_acc("NC_000854.2,NC_000868.1")
    ax3d = plt.figure().add_subplot(projection='3d')
    ax2d = plt.figure().add_subplot()
    for save_path in save_paths:
        record = read(save_path, "genbank")
        # Calculate components of smoothed Z-curve
        plotter = ZCurvePlotter(record)
        n, x, y, _ = plotter.z_curve(window=1000)
        zp, _ = plotter.z_prime_curve(window=1000, return_n=False)
        # Matplotlib 2D display
        ax2d.plot(n[::10], x[::10], label=f"{record.id} RY-disparity")
        ax2d.plot(n[::10], y[::10], label=f"{record.id} MK-disparity")
        ax2d.plot(n[::10], zp[::10], label=f"{record.id} Z'n curve")
        ax2d.legend()
        # Matplotlib 3D display
        ax3d.plot(x[::10], y[::10], zp[::10], label=f"{record.id} Z-curve")
        ax3d.legend()
    plt.show()
    ```
    (2) Commandline usage:  
    For plotting curves in 2D mode:
    ```bash
    zcurve-plotter -a NC_000854.2,NC_000868.1 -s settings.json -p curves.png -o curves_2d.json
    ```
    and for plotting curves in 3D mode:
    ```bash
    zcurve-plotter-3d -a NC_000854.2,NC_000868.1 -s settings.json -p curves.png -o curves_3d.json
    ```
    where the settings should be a JSON like:
    ```json
    {
        "plotter": [
            {
                "window": 10000, 
                "intv": 100,
                "curve2d": "RY,MK,ZP",
                "curve3d": "RY:MK:ZP"
            },
            {
                "window": 10000, 
                "intv": 100,
                "curve2d": "RY,MK,ZP",
                "curve3d": "RY:MK:ZP"
            }
        ]
    }
    ```
    Note that the Z-curve Plotter's 3D mode allows you to select 3 of the 11 curves as components of x,y, and z.  
    For more help information about the setting file, please enter:

    ```bash
    zcurve-plotter --help
    ```
2. Extract Z-curve parameter features  
    (1) Python API implementation:  

    ```python
    from ZCurvePy.RunnableScriptsUtil import download_acc, extract_CDS
    save_paths = download_acc("NC_000854.2")
    records = extract_CDS(save_paths[0])

    from ZCurvePy import ZCurveEncoder
    def encoding(record):
        """ simple batch processing """
        encoder, feature = ZCurveEncoder(record), []
        # Calculate and concatenate 765-bit Z-curve transform
        feature += encoder.mononucl_phase_transform(freq=True)
        feature += encoder.dinucl_phase_transform(freq=True)
        feature += encoder.trinucl_phase_transform(freq=True)
        feature += encoder.k_nucl_phase_transform(k=4, freq=True)
        return feature
    
    features = [encoding(record) for record in records]
    ```

    or use another more powerful API to implement multi-threading:

    ```python
    from ZCurvePy import BatchZCurveEncoder
    # Define the hyper-paramsfor 765-bit Z-curve transform
    hyper_params = [
        {"k": 1, "freq": True}  # Same as mononucl_phase_transform(freq=True)
        {"k": 2, "freq": True}  # Same as dinucl_phase_transform(freq=True)
        {"k": 3, "freq": True}  # Same as trinucl_phase_transform(freq=True)
        {"k": 4, "freq": True}  # Same as k_nucl_phase_transform(k=4, freq=True)
    ]
    encoder = BatchZCurveEncoder(hyper_params, n_jobs=8)
    features = encoder(records)
    ```
    (2) Commandline usage:
    ```bash
    zcurve-encoder -a NC_000854.2 -s settings.json -e True -o features.csv
    ```
    where the setting file should be a JSON like:
    ```json
    {
        "encoder": {
            "hyper_params": [
                {"k": 1, "freq": true},
                {"k": 2, "freq": true},
                {"k": 3, "freq": true},
                {"k": 4, "freq": true}
            ],
            "n_jobs": 8
        }
    }
    ```
    For more help information about the setting file, please enter:
    ```bash
    zcurve-encoder --help
    ```
3. Segmentation for DNA sequences
    Python API implementation:
    ```python
    from ZCurvePy.RunnableScriptsUtil import download_acc
    from Bio.SeqIO import read
    from ZCurvePy import ZCurveSegmenter, ZCurvePlotter
    import matplotlib.pyplot as plt
    # Download data
    path = download_acc("CP001956.1")
    record = SeqIO.read(path[0], "gb")
    # Segmentation
    segmenter = ZCurveSegmenter(mode='WS', min_len=50000)
    seg_points = segmenter.run(record)
    # Calculate z' curve for visualization
    plotter = ZCurvePlotter(record)
    n, zp, _ = plotter.z_prime_curve()
    # Visualization
    for point, _ in seg_points:
        plt.axvline(point)
    plt.plot(x)
    plt.show()
    ```
    Commandline usage:
    ```bash
    zcurve-segmenter -a CP001956.1 -m WS -l 50000 -o seg_points.csv -s True
    ```
4. Build a simple gene recognizer  
    This is an example of training a gene recognition model for *Escherichia coli* :
    ```python
    # We recommend turning on the acceleration system on Intel platforms
    from sklearnex import patch_sklearn
    patch_sklearn()
    from ZCurvePy.RunnableScriptsUtil import download_acc, extract_CDS
    from ZCurvePy import ZCurveBuilder
    from Bio.SeqIO import read, parse
    # Load positive dataset
    path = download_acc("NC_000913.3")[0]
    pos_dataset = extract_CDS(path)
    builder = ZCurveBuilder(standard=True, n_jobs=8)
    builder.fit(pos_dataset)
    # Some sample sequences
    records = parse("samples.fa", "fasta")
    results = builder.predict(records)
    ```
