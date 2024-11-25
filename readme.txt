Hadoop word count 

import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;

import java.io.IOException;

public class WordCountMapper extends Mapper<Object, Text, Text, IntWritable> {
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    @Override
    protected void map(Object key, Text value, Context context) throws IOException, InterruptedException {
        String[] words = value.toString().split("\\s+");
        for (String w : words) {
            word.set(w);
            context.write(word, one);
        }
    }
}

import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Reducer;

import java.io.IOException;

public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
    @Override
    protected void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
            sum += val.get();
        }
        context.write(key, new IntWritable(sum));
    }
}


import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCountDriver {
    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "word count");
        job.setJarByClass(WordCountDriver.class);
        job.setMapperClass(WordCountMapper.class);
        job.setReducerClass(WordCountReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}


Spark


from pyspark import SparkContext

# Initialize SparkContext
sc = SparkContext("local", "Word Count")

# Read input file
input_file = sc.textFile("input.txt")

# Split lines into words
words = input_file.flatMap(lambda line: line.split(" "))

# Create key-value pairs (word, 1)
word_pairs = words.map(lambda word: (word, 1))

# Count occurrences of each word
word_counts = word_pairs.reduceByKey(lambda a, b: a + b)

# Save output to file
word_counts.saveAsTextFile("output_word_count")

# Stop the SparkContext
sc.stop()

#include <iostream>

// Kernel function to run on the GPU
__global__ void helloWorld() {
    printf("Hello, World from GPU thread %d!\n", threadIdx.x);
}

int main() {
    // Launch the kernel with 1 block and 10 threads
    helloWorld<<<1, 10>>>();

    // Wait for the GPU to finish
    cudaDeviceSynchronize();

    return 0;
}
