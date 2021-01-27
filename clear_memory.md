https://www.tecmint.com/clear-ram-memory-cache-buffer-and-swap-space-on-linux/


type this on the linux terminal 

sync; echo 3 > sudo /proc/sys/vm/drop_caches


sync; sudo sh -c "echo 3 > /proc/sys/vm/drop_caches"

then to view memory space
free -m