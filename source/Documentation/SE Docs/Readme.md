import numpy as np

class SpatialPooler:
    def __init__(self, input_size, column_count):
        self.input_size = input_size
        self.column_count = column_count
        self.connections = np.random.rand(input_size, column_count)
        self.threshold = 0.5

    def compute_overlap(self, input_pattern):
        overlap = np.dot(input_pattern, self.connections)
        return overlap

    def inhibit_columns(self, overlap):
        active_columns = np.where(overlap > self.threshold)[0]
        return active_columns

class SDRReconstructor:
    def __init__(self, input_size, column_count):
        self.input_size = input_size
        self.column_count = column_count

    def reconstruct_input(self, active_columns):
        input_pattern = np.zeros(self.input_size)
        input_pattern[active_columns] = 1
        return input_pattern