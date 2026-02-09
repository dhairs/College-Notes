## Use for DMA

Imagine we have an I/O bus and need to be able to communicate to it.

Normally, you'd be manually sending data packets to the device, waiting for it respond, and then starting some request again. This involves polling, so we waste CPU cycles on waiting for the peripheral to respond, and we have to wait for it to be ready as well. 

Instead, we can use DMA. We share some memory between the host and the peripheral device, and we send requests for DMA transfers to the peripheral by writing to a memory region that the DMA controller can read. The DMA controller can then handle sending that request to the device in the background while the CPU returns to doing its own work. Then, the DMA controller allows the peripheral to write directly to some host memory and mark the end of its DMA transfer. Consequently, instead of doing polling, our CPU can set up an interrupt to read from the DMA interface whenever a transfer is completed. This allows the CPU to not waste CPU time for the I/O bound tasks.
