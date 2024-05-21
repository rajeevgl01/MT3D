# GeometricDreamer: Geometry based Text-to-3D Generation using Gaussian Splatting

### Instructions:
1. Install the requirements:
```
pip install -r requirements.txt
```
2. Build the extension for Gaussian Splatting:
```
cd gs
./build.sh
```
3. Start training!
```python
python main.py --config-name=base prompt.prompt="<prompt>"
```
You can specify a different prompt for Point-E:
```python
python main.py --config-name=base prompt.prompt="<prompt>" init.prompt="<point-e prompt>"
```

### Viewer
#### splat viewer
We support [splat](https://github.com/antimatter15/splat) viewer now !
Click the captions of text-to-3D results in our project page to watch the assets in a WebGL based viwer.
[Example: a pineapple](https://gsgen3d.github.io/viewer.html?url=A_zoomed_out_DSLR_photo_of_DSLR_photo_of_a_pineapple.splat).
This great viewer achieves > 40 FPS on my MacBook with M1 pro chip.

#### viser based viewer (Visualize checkpoints on your own computer)
Start the Viewer by:
```python
python vis.py <path-to-ckpt> --port <port>
```
If you are training on servers, [tunneling the port using SSH](https://www.ssh.com/academy/ssh/tunneling-example)
```bash
ssh -L <your_local_port>:<your_server_ip>:<your_server_port> <your_username>@<your_server>
```
then open the viewer in your host computer on port `<your_local_port>`.

### Exports
First set the `PYTHONPATH` env var:
```bash
export PYTHONPATH="."
```
#### To `.ply` file
```bash
python utils/export.py <your_ckpt> --type ply
```
#### To `.splat` file
```bash
python utils/export.py <your_ckpt> --type splat
```
#### To mesh (Currenly only support shape export)
```bash
python utils/export.py <your_ckpt> --type mesh --batch_size 65536 --reso 256 --K 200 --thresh 0.1
```
where the <your_ckpt> can be the path to the .pt checkpoint file or, more conveniently, can be the id for the run (the display name of the run in wandb, e.g. `0|213630|2023-10-11|a_high_quality_photo_of_a_corgi`). The exported files are reside in the `exports/<export-type>`.
