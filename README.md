# Zeepops — AI Product Photoshoots (Bulk)

Zeepops is a tool to generate professional product photoshoots at scale using open-source AI models. Provide product images and metadata in bulk and get consistent, retouched, and variant product photos ready for e-commerce.

## Key features
- Bulk processing of product images (folder or CSV)
- Consistent styling and background across SKUs
- Automatic segmentation, background removal, color correction, and retouching
- Variant generation: hero shots, thumbnails, angled views, lifestyle mockups
- Upscaling and restoration for high-resolution output
- Configurable pipeline and model selection
- Local/self-hostable — no mandatory third-party APIs

## Quick start
1. Prepare input
   - Folder of source images named by SKU or a CSV with rows: sku,image_path,title,category

2. Configure
   - Edit the config file or pass CLI flags to set style, variants, models, and output path

3. Run (example)
```sh
ai-photoshoot --input .\images --config .\photoshoot.config.json --output .\out
```

## Input formats
- Folder: images per SKU
- CSV: rows with product metadata and image paths

## Output
- Structured output directory with subfolders per SKU or batch
- Multiple variants per product and JSON metadata describing transformations

## Open-source models and libraries
This project uses only open-source models and libraries for all image processing steps (segmentation, matting, background removal, style transfer, variant generation, upscaling, and restoration). The pipeline is model-agnostic and supports different checkpoints and inference backends (PyTorch, ONNX, ONNX Runtime, TensorRT).

Common example components:
- Segmentation / matting: Segment Anything (SAM), U^2-Net
- Background & style: Stable Diffusion (+ ControlNet for pose/structure guidance)
- Depth / 3D-aware effects: MiDaS / DPT
- Upscaling & restoration: Real-ESRGAN, SwinIR
- Face/feature restoration: GFPGAN (optional)
- Image primitives & tools: OpenCV, Pillow, ImageMagick
- Hosting & tooling: Hugging Face transformers / diffusers, PyTorch, ONNX

Why open-source
- Reproducibility and auditability
- Flexibility to swap or fine-tune models
- Control over deployment and costs (self-host inference)

## Configuring models
The config accepts model identifiers or file paths. Example keys:
- segmentationModel: "facebook/sam-vit-base" or ".\models\sam.pt"
- diffusionModel: "runwayml/stable-diffusion-v1-5" or local checkpoint
- upscaler: "real-esrgan" or ".\models\realesrgan.onnx"

Use environment variables for tokens if accessing private model hubs.

## Licensing & attribution
- Verify and respect the license of every model checkpoint you use (Apache-2.0, MIT, CreativeML OpenRAIL, etc.)
- Include model license and source in deployment or distribution docs

## Security & privacy
- Keep source images private by self-hosting inference
- Sanitize metadata before sharing
- Maintain processing logs for traceability

## Tips
- Start with a small sample batch to tune prompts, control nets, and upscaling settings
- Keep originals for re-processing
- Use consistent photography to improve results

## Example config (keys)
```json
{
  "style": "white",
  "variants": ["hero","thumbnail","angle"],
  "segmentationModel": "facebook/sam-vit-base",
  "diffusionModel": "runwayml/stable-diffusion-v1-5",
  "upscaler": "realesrgan",
  "output": ".\\out"
}
```

## Contributing
Contributions welcome. Please open issues or pull requests and include model license info for any new checkpoints you add.

## License
Add your project license here.