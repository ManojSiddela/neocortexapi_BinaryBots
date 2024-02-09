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