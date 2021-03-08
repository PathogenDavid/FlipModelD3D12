FlipModel D3D12 Sample Application
======================================================

This fork has the following changes:

* LateSync: Only applicable when "Use Waitable Object" is enabled. Puts the wait right before `Preent` instead of the start of the frame
* AllowTearing: Enables DXGI 1.5 `DXGI_SWAP_CHAIN_FLAG_ALLOW_TEARING`/`DXGI_PRESENT_ALLOW_TEARING` feature. (This totally breaks the present timeline.)
* VisualizeTearing: Alternates the clear color every other frame, which is obviously horrible to those sensitive to flashing lights so enable with caution.
  * If the display is not tearing, the screen will appear red, blue, or purple.
  * If the display is tearing you will see stripes of red and blue.

Some other minor changes:

* Added a workaround for `SetStablePowerState` not working on Windows 10 20H2.
* Updated Visual Studio project to latest toolset and Windows SDK.

--------------------

An interactive visualization for understanding the Direct3D 12 Flip Model.

For a detailed explanation, please see this [article](https://software.intel.com/en-us/articles/sample-application-for-direct3d-12-flip-model-swap-chains).

Build Instructions
==================
FlipModelD3D12.sln contains two projects:
- FlipModelD3D12, for building a regular (win32) desktop application.
- FlipModelUniversal, for building a Windows 10 Universal App.

Choose your start up project, build and run.

Requirements
============
- Windows 10 or greater
- Visual Studio 2015 or higher


 
