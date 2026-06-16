# MitoBox

MitoBox is a versioned sandbox runtime for AI agents.

The project treats each sandbox as a cell. A cell can be restored from a snapshot, run independently,
commit its full state as a new snapshot, and continue along a branch line. The name comes from mitosis:
one state can split into independent execution lines, while each cell remains isolated from the others
