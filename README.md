# recycleAdapter

package se.rickylagerkvist.recycleviewtest;

import android.support.design.widget.Snackbar;
import android.support.v7.widget.RecyclerView;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;

import com.squareup.picasso.Picasso;

import java.util.List;

/**
 * Created by Ricky on 2017-01-29.
 */

public class RecyclerAdapter extends RecyclerView.Adapter<RecyclerAdapter.MyViewHolder>{

    private List<AppModel> mAppModels;

    public class MyViewHolder extends RecyclerView.ViewHolder{

        public TextView title, body, app1, app2;
        public ImageView image;

        public MyViewHolder(final View itemView) {
            super(itemView);

            title = (TextView) itemView.findViewById(R.id.title);
            body = (TextView) itemView.findViewById(R.id.body);
            app1 = (TextView) itemView.findViewById(R.id.app1);
            app2 = (TextView) itemView.findViewById(R.id.app2);
            image = (ImageView) itemView.findViewById(R.id.image);
        }
    }

    public RecyclerAdapter(List<AppModel> mAppModels){
        this.mAppModels = mAppModels;
    }

    @Override
    public RecyclerAdapter.MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View ItemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.applayout, parent, false);
        return new MyViewHolder(ItemView);
    }

    @Override
    public void onBindViewHolder(RecyclerAdapter.MyViewHolder holder, int position) {
        final AppModel appModel = mAppModels.get(position);
        holder.title.setText(appModel.getTitle());
        holder.body.setText(appModel.getBody());
        holder.app1.setText(appModel.getFirstAppName());
        holder.app2.setText(appModel.getSecondAppName());

        Picasso.with(holder.image.getContext())
                .load(R.drawable.pic2)
                .resize(holder.image.getWidth(),200)
                .into(holder.image);

        holder.app1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar.make(view, appModel.getFirstAppName(), Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });

        holder.app2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar.make(view, appModel.getSecondAppName(), Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });
    }

    @Override
    public int getItemCount() {
        return mAppModels.size();
    }

}
