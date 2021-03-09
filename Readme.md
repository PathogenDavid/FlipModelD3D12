FlipModel D3D12 Sample Application
======================================================

This fork has the following changes:

* LateSync: Only applicable when "Use Waitable Object" is enabled. Puts the wait right before `Present` instead of the start of the frame
* AllowTearing: Enables DXGI 1.5 `DXGI_SWAP_CHAIN_FLAG_ALLOW_TEARING`/`DXGI_PRESENT_ALLOW_TEARING` feature. (This totally breaks the present timeline.)
* VisualizeTearing: Alternates the clear color every other frame, which is obviously horrible to those sensitive to flashing lights so enable with caution.
  * If the display is not tearing, the screen will appear red, blue, or purple.
  * If the display is tearing you will see stripes of red and blue.
* MaximumFrameLatency2: Poorly named, but allows changing the maximum frame latency without recreating the swap chain.
  * Added to see behavior since A) the Intel sample didn't allow it and B) I had seen on the DirectX Discord that it didn't work.
  * [The documentation](https://docs.microsoft.com/en-us/windows/win32/api/dxgi1_3/nf-dxgi1_3-idxgiswapchain2-setmaximumframelatency) makes no mention about needing to do this during swapchian creation and doing it after the swap chain has been used doesn't result in any errrors, so that seemed fishy to me.
  * With a naive implementation, it seems like you're allowed to increase the maxmimum latency, but not lower it. (Lowering it does not seem to lower the effective latency.)
  * I'm fairly certain what is happening is that the handle is only waited on once per present, but when you decrease the maximum latency the internals of the handle get stuck one frame in the past.
  * To fix it, you (seemingly) just need to wait on the handle for every frame of maximum latency you removed.
  * Note: The number in the HUD next to MaximumFrameLatency2 is the one actually in use. Change the normal MaximumLatency to recreate the swap chain with that latency.

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


 
