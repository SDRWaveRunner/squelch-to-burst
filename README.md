# Squelch to burst
This set of scripts is basically a embedded python-block [[1]] to convert tags.

### Background
When using a squelch in a GNUradio flowgraph the power squelch block [[2]] emits tags to mention the state:

-- **squelch\_sob** for the start of the burst<br>
-- **squelch\_eob** for the end of the burst<br>

When using a tagged filesink [[3]], this sink expects another tag:

-- **burst** value True for the start of the burst<br>
-- **burst** value False for the end of the burst<br>

This embedded python block tries to match these together.


### Mapping tags
The initial idea was to translate tags and let the user select the source and destination tag. This causes some problems:

1. The squelch to burst mapping is not a 1-to-1 mapping: Both squelch\_sob and squelch\_eob maps to burst but only the value changes from True to False
2. There is no "Delete Tag" option found [[4]]. Thus adding a tag is the only way to solve this.

So a fixed squelch to burst mapping is made.

### Flowgraphs

1. **squelch\_to\_burst.grc** is a audio recorder. When hitting the squelch, a new file is made.
2. **read\_back\_nbfm.grc** plays back a recorded IQ file from a SSTV transmission from ISS. When hitting the squelch, a new file with raw audio-samples is made. The squelch is not perfect here yet.

### ToDo
- [ ] Test in Gnuradio 3.8
- [ ] Seprate the block and include it in GNUradio


---
[1]: https://wiki.gnuradio.org/index.php/Embedded_Python_Block
[2]: https://wiki.gnuradio.org/index.php/Power_Squelch
[3]: https://wiki.gnuradio.org/index.php/Tagged_File_Sink
[4]: https://www.gnuradio.org/doc/doxygen/page_stream_tags.html#stream_tags_api