**中文版本 [中文](README_zh.md)**

# Unique3D
Official implementation of Unique3D: High-Quality and Efficient 3D Mesh Generation from a Single Image

[Kailu Wu](https://scholar.google.com/citations?user=VTU0gysAAAAJ&hl=zh-CN&oi=ao), [Fangfu Liu](https://liuff19.github.io/), Zhihan Cai, Runjie Yan, Hanyang Wang, Yating Hu, [Yueqi Duan](https://duanyueqi.github.io/), [Kaisheng Ma](https://group.iiis.tsinghua.edu.cn/~maks/)

## [Paper](https://arxiv.org/abs/2405.20343) | [Project page](https://wukailu.github.io/Unique3D/) | [Huggingface Demo](https://huggingface.co/spaces/Wuvin/Unique3D) | [Gradio Demo](https://u45213-bcf9-ef67553e.westx.seetacloud.com:8443/) | [Online Demo](https://www.aiuni.ai/)

* Demo inference speed: Gradio Demo > Huggingface Demo > Huggingface Demo2 > Online Demo

**If the Gradio Demo unfortunately hangs or is very crowded, you can use the Online Demo [aiuni.ai](https://www.aiuni.ai/), which is free to try (get the registration invitation code Join Discord: https://discord.gg/aiuni). However, the Online Demo is slightly different from the Gradio Demo, in that the inference speed is slower, and the generation results is less stable, but the quality of the material is better.**

<p align="center">
    <img src="assets/teaser_safe.jpg">
</p>

High-fidelity and diverse textured meshes generated by Unique3D from single-view wild images in 30 seconds.

## More features 

The repo is still being under construction, thanks for your patience. 
- [x] Upload weights.
- [x] Local gradio demo.
- [ ] Detailed tutorial.
- [x] Huggingface demo.
- [ ] Detailed local demo.
- [x] Comfyui support.
- [x] Windows support.
- [ ] Docker support.
- [ ] More stable reconstruction with normal.
- [ ] Training code release.

## Preparation for inference

### Linux System Setup.
```angular2html
conda create -n unique3d
conda activate unique3d
pip install -r requirements.txt
```

### Windows Setup.

* Thank you very much `jtydhr88` for the windows installation method! See [issues/15](https://github.com/AiuniAI/Unique3D/issues/15).

According to [issues/15](https://github.com/AiuniAI/Unique3D/issues/15), implemented a bat script to run the commands, so you can:
1. Might still require Visual Studio Build Tools, you can find it from [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/?q=build+tools).
2. Create conda env and activate it
   1. `conda create -n unique3d-py311 python=3.11`
   2. `conda activate unique3d-py311`
3. download [triton whl](https://huggingface.co/madbuda/triton-windows-builds/resolve/main/triton-2.1.0-cp311-cp311-win_amd64.whl) for py311, and put it into this project.
4. run **install_windows_win_py311_cu121.bat**
5. answer y while asking you uninstall onnxruntime and onnxruntime-gpu
6. create the output folder **tmp\gradio** under the driver root, such as F:\tmp\gradio for me.
7. python app/gradio_local.py --port 7860

More details prefer to [issues/15](https://github.com/AiuniAI/Unique3D/issues/15).

### Interactive inference: run your local gradio demo.

1. Download the weights from [huggingface spaces](https://huggingface.co/spaces/Wuvin/Unique3D/tree/main/ckpt) or [Tsinghua Cloud Drive](https://cloud.tsinghua.edu.cn/d/319762ec478d46c8bdf7/), and extract it to `ckpt/*`.
```
Unique3D
    ├──ckpt
        ├── controlnet-tile/
        ├── image2normal/
        ├── img2mvimg/
        ├── realesrgan-x4.onnx
        └── v1-inference.yaml
```

2. Run the interactive inference locally.
```bash
python app/gradio_local.py --port 7860
```

## ComfyUI Support

Thanks for the [ComfyUI-Unique3D](https://github.com/jtydhr88/ComfyUI-Unique3D) implementation from jtydhr88!

## Tips to get better results

1. Unique3D is sensitive to the facing direction of input images. Due to the distribution of the training data, orthographic front-facing images with a rest pose always lead to good reconstructions.
2. Images with occlusions will cause worse reconstructions, since four views cannot cover the complete object. Images with fewer occlusions lead to better results.
3. Pass an image with as high a resolution as possible to the input when resolution is a factor.

## Acknowledgement

We have intensively borrowed code from the following repositories. Many thanks to the authors for sharing their code.
- [Stable Diffusion](https://github.com/CompVis/stable-diffusion)
- [Wonder3d](https://github.com/xxlong0/Wonder3D)
- [Zero123Plus](https://github.com/SUDO-AI-3D/zero123plus)
- [Continues Remeshing](https://github.com/Profactor/continuous-remeshing)
- [Depth from Normals](https://github.com/YertleTurtleGit/depth-from-normals)

## Collaborations
Our mission is to create a 4D generative model with 3D concepts. This is just our first step, and the road ahead is still long, but we are confident. We warmly invite you to join the discussion and explore potential collaborations in any capacity. <span style="color:red">**If you're interested in connecting or partnering with us, please don't hesitate to reach out via email (wkl22@mails.tsinghua.edu.cn)**</span>.

- Follow us on twitter for the latest updates: https://x.com/aiuni_ai
- Join AIGC 3D/4D generation community on discord: https://discord.gg/aiuni
- Research collaboration, please contact: ai@aiuni.ai

## Citation

If you found Unique3D helpful, please cite our report:
```bibtex
@misc{wu2024unique3d,
      title={Unique3D: High-Quality and Efficient 3D Mesh Generation from a Single Image}, 
      author={Kailu Wu and Fangfu Liu and Zhihan Cai and Runjie Yan and Hanyang Wang and Yating Hu and Yueqi Duan and Kaisheng Ma},
      year={2024},
      eprint={2405.20343},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
