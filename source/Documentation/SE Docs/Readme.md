Now i wanted to change  by adding a sparsity parameter to the SpatialPooler class constructor, allowing for the specification of the desired sparsity level.
Modified the inhibit_columns method to select the top sparsity column_count active columns based on overlap scores, using np.argsort to obtain indices of active columns.
Used the sparsity parameter when initializing the SpatialPooler instance.

class SpatialPooler:
    de_init_(self, input_size, column_count, sparsity=0.2):
        self.input_size = input_size
        self.column_count = column_count
        self.connections = np.random.rand(input_size, column_count)
        self.sparsity = sparsity

        def compute_overlap(self, input_pattern):
        overlap = np.dot(input_pattern, self.connections)
        return overlap

        def inhibit_columns(self, overlap):
        active_columns = np.argsort(overlap)[-int(self.sparsity * self.column_count):]
        return active_columns

class SDRReconstructor:
    def_init_(self, input_size, column_count):
        self.input_size = input_size
        self.column_count = column_count

    def reconstruct_input(self, active_columns):
        input_pattern = np.zeros(self.input_size)
        input_pattern[active_columns] = 1
        return input_pattern

# Create spatial pooler with a specified sparsity
spatial_pooler = SpatialPooler(input_size, column_count, sparsity=0.2)
overlap = spatial_pooler.compute_overlap(input_pattern)
active_columns = spatial_pooler.inhibit_columns(overlap)

# Reconstruct input pattern
sdr_reconstructor = SDRReconstructor(input_size, column_count)
reconstructed_pattern = sdr_reconstructor.reconstruct_input(active_columns)
print("Original Input Pattern:", input_pattern)
print("Reconstructed Input Pattern:", reconstructed_pattern)